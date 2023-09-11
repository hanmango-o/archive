# 입출력 I/O

java에서는 사용자가 키보드 입력시 아래와 같이 Scanner 를 사용하여 값을 읽을 수 있습니다.

```java
import java.util.*;

Scanner sc = new Scanner(System.in);
```

## 타입별 입력
기본적으로 Scanner는 공백을 기준으로 입력받게 되며, 각 타입별 사용은 아래와 같습니다.

### Integer
정수형 데이터를 입력 받고 싶다면, 아래와 같이 사용할 수 있습니다.

```java
Scanner sc = new Scanner(System.in);
int input = sc.nextInt(); 
```

### Double
실수형 데이터를 입력받고 싶다면, 아래와 같이 사용합니다.

```java
Scanner sc = new Scanner(System.in);
double input = sc.nextDouble();
```

### String
문자열 데이터를 입력받고 싶다면, 아래와 같이 사용합니다.
```java
Scanner sc = new Scanner(System.in);
String input = sc.next();
```

만약 공백을 포함하는 문자열을 입력받고 싶다면, 아래와 같이 `nextLine()` 을 사용합니다.

```java
Scanner sc = new Scanner(System.in);
String input = sc.nextLine() // hello world! 같이 공백을 포함한 문자열을 한 줄에 입력받음
```

### Char
java에서 문자를 입력받는 별도의 Scanner 메서드는 없습니다. 따라서 문자형으로 입력받은 이후, 배열의 0번 인덱스로 접근하여 문자를 추출합니다.

```java
Scanner sc = new Scanner(System.in);
String input = sc.next();
char c = input.charAt(0);

// 축약 가능
char c = sc.next().charAt(0);
```


## 특정 문자에 따른 입력
입력받는 값이 특정 문자를 사이에 두고 있다면, 아래와 같은 방법으로 입력을 제어할 수 있습니다.

```java
Scanner sc = new Scanner(System.in);
sc.useDelimiter("특정문자");
// 입력 ...
```

단, useDelimiter 사이에 들어가는 특정 문자 형식은 정규표현식을 지원하기 때문에 정규 표현식 문법에 어긋나서는 안됩니다.

예를 들어 `.` 는 정규 표현식에서 All의 의미이므로 `.` 문자를 기준으로 입력을 받고 싶다면, 아래와 같이 사용해야 합니다.

```java
Scanner sc = new Scanner(System.in);
sc.useDelimiter("\\.");

// 그 외 주의해야 할 문자들
sc.useDelimiter("\\^");
sc.useDelimiter("\\$");
sc.useDelimiter("\\*");
```

