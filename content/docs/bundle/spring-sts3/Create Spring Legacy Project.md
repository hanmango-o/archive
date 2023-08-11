# Create Spring Legacy Project

STS3를 활용한 Spring Legacy Project 를 생성하는 과정에 대해 알아봅니다.


## 들어가기 앞서

먼저 설정한 개발 환경은 아래와 같습니다.

__개발환경__
- Java 11
- Mac M1 (ARM)
- STS3 (v3.9.17.RELEASE)
- Eclipse
- Apache Tomcat (v9.0.x)

위 개발 환경은 이미 설정이 완료된 상태로 진행합니다.


## 스프링 프로젝트 생성

STS3에서 스프링 프로젝트를 생성하는 방법에는 크게 아래 3가지가 있습니다.

1. 처음부터 스프링 프로젝트를 지정하고 생성하는 방식
2. Maven이나 Gradle 프로젝트를 생성한 후 프레임워크를 추가하는 방식
3. 직접 프레임워크 라이브러리를 추가하는 방식

위 3가지 방법 중 1번 방식을 알아봅니다.


### Spring MVC Project

화면 오른쪽 상단의 `File > New > Spring Legacy Project` 를 클릭하여 Maven을 기반으로 하는 여러 Spring 프로젝트를 선택하여 스프링 프로젝트를 생성할 수 있습니다.

![[docs_spring-sts3_1.png]]

이후, 패키지 명을 지정하고 finish 를 눌러 Spring 프로젝트를 생성합니다.

프로젝트를 생성하게 되면 필요한 코드와 라이브러리가 다운로드됩니다. 이때, 다운로드 받은 라이브러리는 `.m2` 라는 폴더의 repository 폴더 안에 추가됩니다.


## 스프링 버전 변경

생성된 스프링 프로젝트의 버전을 변경해야 하는 경우 `pom.xml` 파일을 통해서 변경할 수 있습니다.

Spring Legacy Project 메뉴를 통해 생성한 스프링 프로젝트의 경우 스프링 버전은 3.x 이고, JDK는 1.6을 기준으로 생성되게 됩니다.

```xml
<properties>
	<java-version**>1.6</java-version>
	<org.springframework-version>3.1.1.RELEASE</org.springframework-version>
	<org.aspectj-version>1.6.10</org.aspectj-version>
	<org.slf4j-version>1.6.6</org.slf4j-version>
</properties>
```

스프링 5 버전을 이용할 예정이므로 pom.xml 파일을 수정해줍니다.

스프링과 관련된 버전은 [Maven Repository](https://mvnrepository.com/artifact/org.springframework/)에서 확인할 수 있습니다. 해당 버전을 찾은 후 아래와 같이 수정합니다.

```xml
<properties>
	<java-version**>1.6</java-version>
	<org.springframework-version>5.0.7.RELEASE</org.springframework-version>
	<org.aspectj-version>1.6.10</org.aspectj-version>
	<org.slf4j-version>1.6.6</org.slf4j-version>
</properties>
```

스프링 버전 수정 후 Maven Dependencies 항목을 통해 스프링 프레임워크가 변경되었는지 확인합니다.

![[docs_spring-sts3_2.png]]

## Java 버전 변경

앞서 살펴본 것 처럼 JDK 버전 역시 1.6으로 생성된 것을 알 수 있습니다. 스프링 버전 5의 경우 JDK 1.8 이상을 사용해야 하므로 Java 버전 역시 변경되어야 합니다.

```xml
<properties>
	<java-version**>11</java-version>
	<org.springframework-version>5.0.7.RELEASE</org.springframework-version>
	<org.aspectj-version>1.6.10</org.aspectj-version>
	<org.slf4j-version>1.6.6</org.slf4j-version>
</properties>
```

JDK 환경을 11로 변경했으므로 JRE System Library 역시 변경해야 합니다.
아래와 같이 plugin 태그 중 maven-compiler-plugin의 내용을 11로 변경합니다.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>2.5.1</version>
    <configuration>
	    <source>1.6</source>
        <target>1.6</target>
        <compilerArgument>-Xlint:all</compilerArgument>
        <showWarnings>true</showWarnings>
        <showDeprecation>true</showDeprecation>

    </configuration>
</plugin>
```

모든 변경을 마치고 Maven > Update Project 를 실행하여 변경사항을 업데이트합니다.


## Tomcat을 통한 프로젝트 확인

내장 서버 Tomcat을 활용하여 설정된 프로젝트가 정상적으로 동작하는 지 확인해보겠습니다.

프로젝트의 Run > Run as Server 를 선택 후, Tomcat 9.0 으로 실행합니다. 이후, `http://localhost:8080/controller/` 를 통해 접근하면 정상적으로 동작됨을 알 수 있습니다.


## Lombok 라이브러리 설치

Lombok 라이브러리를 통해 Java 개발 시 자주 사용하는 getter/setter, toString(), 생성자 등을 자동을 생성할 수 있습니다. 이러한 Lombok은 스프링 코드 작성 시 필요한 클래스를 설계할 때 유용하게 사용됩니다.

Lombok은 [Project Lombok](https://projectlombok.org/)에서 jar 파일 형태로 다운로드 받을 수 있습니다.

다른 jar 파일들과는 다르게 프로젝트 코드에서만 사용하는 것이 아닌 이클립스 IDE 내에서도 사용되어야 하기 때문에 사이트에서 별도로 설치해주어야 합니다.

jar 파일 다운로드 후 실행하여 IDE에 Lombok을 설치합니다.