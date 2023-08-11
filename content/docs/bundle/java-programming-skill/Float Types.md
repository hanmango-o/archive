---
title: Integer Types
showToc: true
---

실수 자료형

float
double

부동소수점 개념을 사용하여 integer 와는 값을 담는 개념자체가 다름

double이 더 세밀함
얄코 영상 봐야할듯?

float 도 F 나 f를 적어주어야 함
아니면 double 이라고 인식
float a = 3.14; > double 로 타입 캐스팅되어서 들어감
float a = 3.14f;
float a = (float) 3.14;

정수를 대입할 경우 묵시적 변환됨
long a = 1;
float b = a;
float c = a;
float에도 long 담을 수 있음
단, 정확도는 떨어짐

연산자 다 사용가능

float 끼리의 연산은 float 반환

float + double 은 double 반환
아니면 캐스팅해야함

Bigdecima 클래스 이용해서 연산의 오차없이 계산 가능

리터럴로 작성시 double 임을 명시해주어야 실수로 파악하고 정확히 계산 가능
정수에 .0 을 붙여주면 실수로 파악

실수를 정수로 캐스팅할 경우 소수점 아래 버림

정수와 실수 비교 연산자도 가능

