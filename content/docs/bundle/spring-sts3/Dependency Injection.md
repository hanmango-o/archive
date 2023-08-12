# Dependency Injection

스프링의 가장 중요한 특징 중 하나인 DI에 대해 알아보고, 동작과정을 살펴봅니다.


## 들어가기 앞서

스프링에서는 `생성자를 이용한 주입`과 `setter 메서드를 이용한 주입`을 통해 DI를 구현합니다. 설정 방식에는 `XML` 이나 `어노테이션`을 이용하게 됩니다.

STS3 에서는 XML을 이용한 설정 방식이 기본이므로 XML을 이용한 설정과 `Lombok`, `spring-test` 라이브러리의 초기 설정이 필요합니다.

pom.xml에 아래와 같이 Lombok, spring-test 라이브러리를 추가합니다.

```xml
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-test</artifactId>
	<version>${org.springframework-version}</version>
</dependency>
<dependency>
	<groupId>org.projectlombok</groupId>
	<artifactId>lombok</artifactId>
	<version>1.18.28</version>
	<scope>provided</scope>
</dependency>
```

또한 Log4J 라이브러리의 초기 설정 버전인 1.2.15를 1.2.17로 수정합니다.

```xml
<dependency>
	<groupId>log4j</groupId>
	<artifactId>log4j</artifactId>
	<version>1.2.17</version> // 수정
	...
```


## 예제 클래스 생성 및 설정

기존 ex00 프로젝트에 org.mango.sample 패키지를 생성하고 아래와 같이 Restaurant 클래스와 Chef 클래스를 생성합니다.

```java
package com.mango.sample;

import org.springframework.stereotype.Component;

import lombok.Data;

@Component
@Data
public class Chef {
}
```

```java
package com.mango.sample;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

import lombok.Data;
import lombok.Setter;

@Component
@Data
public class Restaurant {

    @Setter(onMethod = @__({ @Autowired }))
    private Chef chef;

}
```

작성된 코드는 Restaurant 객체는 Chef 타입의 객체가 필요로 한다라는 상황입니다. 사용한 어노테이션에 대한 설명은 아래와 같습니다.

- @Component : 스프링에게 해당 클래스가 스프링에서 관리해야 하는 대상임을 표시합니다.
- @Setter : 자동으로 setChef()를 컴파일 시 생성합니다.
	- onMethod : 생성된 setter에 @Autowired 어노테이션을 추가하는 속성입니다.

Lombok에 의해 생성된 클래스에 대한 정보는 아래와 같습니다.

![[docs_spring-sts3_4.png]]

### XML을 통한 DI 설정
스프링은 클래스에서 객체를 생성하고 객체들의 의존성에 대한 처리 작업을 내부에서 처리합니다. 이렇게 스프링에 의해 관리되는 객체를 빈(Bean)이라 하며, 이에 대한 설정은 XML 또는 Java를 통해 관리할 수 있습니다.

프로젝트의 src 폴더에 root-context.xml 파일은 Bean을 설정하는 설정 파일입니다. 설정을 위한 과정은 아래와 같습니다.

1. root-context.xml 파일에서 NameSpace 탭을 클릭하고 context 항목을 체크합니다.
2. 이후 source 탭에서 아래의 코드를 추가합니다.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans
	xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/beans https://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.3.xsd">
	<!-- Root Context: defines shared resources visible to all other web components -->
	<context:component-scan base-package="org.mango.sample"></context:component-scan> // 추가
</beans>
```

Bean Graph를 선택하면 Restaurant와 Chef 객체가 설정된 것을 확인할 수 있습니다.

![[docs_spring-sts3_5.png]]


## 동작 과정
앞서 작성한 예제가 스프링의 동작시 어떻게 작동하는 알아보겠습니다.

1. 스프링 프레임워크 실행 시, 스프링이 사용하는 메모리 영역인 Context가 만들어지게 됩니다. 이때 스프링에서는 ApplicationContext라는 객체가 만들어집니다.

2. root-context.xml에 설정되어 있는 `<context:component-scan>`태그의 내용을 통해 `org.mango.sample` 패키지를 스캔(Scan)합니다.

> [!Info] 
> 스프링은 자신이 객체를 생성하고 관리해야 하는 객체들에 대한 설정이 필요합니다. 따라서 이에 대한 설정 파일인 root-context.xml 을 먼저 살펴보게 됩니다.

3. 해당 패키지에 있는 클래스들 중에서 @Component 라는 어노테이션이 존재하는 클래스의 인스턴스를 생성합니다.

4. Restaurant 객체는 Chef 객체가 필요하다는 의미의 @Autowired 설정이 되어 있으므로, 스프링은 Chef 객체의 레퍼런스를 Restaurant 객체에 주입합니다.


### 테스트 코드를 통한 확인
위 과정이 동작되는 것을 테스트 코드를 통해 살펴보겠습니다.

프로젝트의 scr/test/java 폴더에 org.mango.sample.SampleTests 클래스를 생성하고 아래와 같이 코드를 작성합니다.

```java
package org.mango.sample;

import static org.junit.Assert.assertNotNull;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;

import lombok.Setter;
import lombok.extern.log4j.Log4j;

@RunWith(SpringJUnit4ClassRunner.class) (1)
@ContextConfiguration("file:src/main/webapp/WEB-INF/spring/root-context.xml") (2)
@Log4j (3)
public class SampleTests {

    @Setter(onMethod = @__({
        @Autowired (4)
    }))
    private Restaurant restaurant;

    @Test (5)
    public void testExist() {
        assertNotNull(restaurant); (6)

        log.info(restaurant);
        log.info("---------------------");
        log.info(restaurant.getChef());
    }

}
```

SampleTests 클래스는 spring-test 모듈을 이용하여 간단하게 스프링을 동작시키고, 앞서 설명한 동작들이 일어나는 것을 확인합니다.

> [!caution] 
> 이때, Junit은 4.12 이상의 버전을 사용하여야 합니다.


위 코드에 대한 설명은 아래와 같습니다.

1. 현재 테스트 코드가 스프링을 실행하는 역할을 할 것이라고 명시하는 @RunWith 어노테이션입니다.

2. @ContextConfiguration은 지정된 클래스나 문자열을 이용해서 필요한 객체들을 스프링의 Bean으로 등록하게 됩니다. 이때 사용하는 문자열은 classpath: 나 file: 을 이용할 수 있습니다.

3. @Log4j 는 Lombok을 이용하여 로그를 기록하는 Logger를 변수로 생성합니다. 별도의 Logger 객체의 선언이 없어도(`Logger log = new Logger();`) Log4j 라이브러리와 설정이 존재한다면, 위 예제에서의 `log.info(restaurant);` 와 같이 바로 사용할 수 있습니다.

> [!More] 
> 해당 로그에 대한 설정은 `src/main/resources` 와 `src/test/resources` 에 별도로 존재합니다.
> Spring Legacy Project 로 프로젝트를 생성한 경우 Log4j와 해당 설정이 완료된 상태로 생성되기 떄문에 별도의 설정이 필요하지 않습니다.

4. @Autowired는 해당 인스턴스 변수가 스프링으로부터 자동으로 주입해 달라는 표시입니다.

5. @Test는 JUnit에서 테스트 대상을 표시하는 어노테이션입니다. 해당 메서드를 선택하고 JUnit Test 기능을 실행합니다.

6. assertNotNull() 은 null이 아니여야만 테스트가 성공한다는 것을 의미합니다.

위 테스트 코드의 실행 결과는 아래와 같습니다.

```
...

INFO : org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor - JSR-330 'javax.inject.Inject' annotation found and supported for autowiring
INFO : org.mango.sample.SampleTests - Restaurant(chef=Chef())
INFO : org.mango.sample.SampleTests - ---------------------
INFO : org.mango.sample.SampleTests - Chef()
INFO : org.springframework.context.support.GenericApplicationContext
```

위 실행 결과에서 주목해야 하는 부분은 아래와 같습니다.

- new Restaurant() 와 같은 객체 생성이 없음에도 객체가 만들어졌습니다. 이는 스프링이 관리가 필요한 Bean을 어노테이션 등을 이용해 생성, 관리하는 일종의 컨테이너 나 팩토리 기능을 가지고 있다는 것을 의미합니다.
- @Data 어노테이션으로 Lombok을 이용하여 객체가 생성되었다는 것을 알 수 있습니다.
- Chef 인스턴스 변수 타입에 Chef 타입의 객체가 주입되었다는 것을 알 수 있습니다. 이는 스프링의 @Autowired와 같은 어노테이션을 이용하여 객체를 직접 관리하지 않아도 됨을 의미합니다.

이러한 테스트 결과는 스프링의 핵심이라고 할 수 있습니다.

1. 테스트 코드가 실행되기 위해 스프링 프레임워크가 동작되었다는 점
2. 동작 과정에서 필요한 객체를이 스프링에 등록되었다는 점
3. DI가 필요한 객체가 자동으로 주입되었다는 점


## 어노테이션 정리

앞서 살펴본 예제에서 사용한 어노테이션을 정리하면 아래와 같습니다.

| Lombok 관련 | Spring 관련 | 테스트 관련           |
| ----------- | ----------- | --------------------- |
| @Setter     | @Autowired  | @RunWith              |
| @Data       | @Component  | @ContextConfiguration |
| @Log4j      |             | @Test                 |


### Lombok 관련
Lombok은 컴파일 시 흔하게 작성되는 코드를 완성해주는 라이브러리입니다.

#### @Setter
@Setter 어노테이션은 setter 메서드를 생성하는 역할을 수행합니다. @Setter에는 아래 3가지 속성을 사용할 수 있습니다.

| 속성     | 의미                                                       |
| -------- | ---------------------------------------------------------- |
| value    | 접근 제한 속성을 의미, default = lombok.AccessLevel.PUBLIC |
| onMethod | setter 메서드의 생성 시 메서드에 추가할 어노테이션 지정    |
| onParam  | setter 메서드의 파라미터에 어노테이션을 사용하는 경우      |

#### @Data
@Data 어노테이션은 Lombok에서 가장 자주 사용되는 어노테이션입니다.

@ToString, @EqualsAndHashCode, @Getter/@Setter, @RequiredArgsConstructor 를 모두 포함하는 어노테이션으로 @Data 를 사용한다면 위 어노테이션을 통해 생성할 수 있는 모든 메서드를 생성할 수 있습니다.

> [!more]
> Restaurant에 getChef() 메서드 역시 @Data 메서드를 통해 생성된 것임을 알 수 있습니다.

#### @Log4j
@Log4j 어노테이션은 로그 객체를 생성합니다. 이에 별도의 Logger 객체의 선언 없이도 log 변수를 사용할 수 있게 됩니다.


### Spring 관련

#### @Component
@Component 어노테이션은 해당 클래스가 스프링에서 객체로 만들어서 관리하는 대상임을 명시하는 어노테이션입니다.

@Component가 있는 클래스를 스프링이 읽을 수 있도록 root-context.xml에 component-scan을 통해 지정되어 있기 때문에 해당 클래스들을 객체로 생성하여 Bean으로 관리할 수 있습니다.

#### @Autowired
@Autowired 어노테이션은 스프링 내부에서 자신이 특정한 객체에 의존적이므로 자신에게 해당 타입의 Bean을 주입해달라는 의미입니다.

스프링은 @Autowired 를 보고 스프링 내부에 등록된 Bean 중 적당한 것을 골라 자동으로 주입합니다. 만약 필요한 객체가 Bean으로 관리되지 않는다면 에러가 발생하게 됩니다.


### 테스트 관련

#### @RunWith
@RunWith 어노테이션은 테스트 시 필요한 클래스를 지정합니다.

#### @ContextConfiguration
@ContextConfiguration 어노테이션은 테스트와 관련된 가장 중요한 어노테이션입니다.
스프링이 실행되면서 어떤 설정 정보를 읽어 들여야 하는지를 명시합니다.

locations 속성을 이용하여 문자열의 배열로 XML 설정 파일을 명시할 수도 있고, classes 속성으로 @Configuration이 적용된 클래스를 지정해 줄 수도 있습니다.

#### @Test
@Test 어노테이션은 jUnit에서 해당 메서도가 jUnit 상의 단위 테스트의 대상인지 알려줍니다.


## 단일 생성자의 묵시적 주입

