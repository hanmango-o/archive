# Spring Project 구조

STS3에서 Spring Legacy Project 메뉴를 통해 생성된 프로젝트의 구조에 대해 알아봅니다.


## 프로젝트 구조

생성된 프로젝트의 주요 폴더 구조는 아래와 같습니다.

```
.
├── src
│   ├── main
│   │   ├── java
│   │   ├── resources
│   │   │   ├── META-INF
│   │   │   └── log4j.xml
│   │   └── webapp
│   │       ├── WEB-INF
│   │       │   ├── classes
│   │       │   ├── spring
│   │       │   │   ├── appServlet
│   │       │   │   │   └── servlet-context.xml
│   │       │   │   └── root-context.xml
│   │       │   ├── views
│   │       │   │   └── home.jsp
│   │       │   └── web.xml
│   │       └── resources
│   └── test
│       ├── java
│       └── resources
│           └── log4j.xml
└── pom.xml
```

각 폴더에 대한 설명은 아래와 같습니다.

- src/main/java
	- 작성되는 코드의 경로
- src/main/resources
	- 실행할 때 참고하는 기본 경로(주로 설정 파일)
- src/test/java
	- 테스트 코드를 넣는 경로
- src/test/resources
	- 테스트 관련 설정 파일 보관 경로
- src/main/WEB-INF/spring/appServlet/servlet-context.xml
	- 웹과 관련된 스프링 설정 파일
- src/main/WEB-INF/spring/root-context.xml
	- 스프링 설정 파일
- src/main/WEB-INF/views
	- 템플릿 프로젝트의 jsp 파일 경로
- src/main/WEB-INF/web.xml
	- Tomcat의 web.xml 파일
- pom.xml
	- Maven의 pom.xml 파일