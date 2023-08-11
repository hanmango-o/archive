---
showToc: true
---

# Swift Basic

----

## Chap01. 

상수 선언 키워드 let
변수 선언 키워드 var

상수 선언
let 이름 : 타입  = 값

변수 선언
var 이름 : 타입 = 값

값의 타입이 명확하다면 타입 생략
let 이름 = 값
var 이름 = 값

선언 후 나중에 값 할당도 가능
let 이름 : 타입 // 타입 반드시 명시
var 이름 : 타입 // ㅇㅇ

이름 = 값


기본 데이터 타입
Bool
true, false
0, 1 > 사용 안됨 Int 로 인식

Int
64bit 정수형 타입

UInt
Unsigned Integer : 부호가 없는 정수(양의 정수)
var s : UInt = 100
Int 는 넣을 수 없음
var a : Int
s = a // error

Float
Double

Character
"" 사용

String
character 자료 교환 안됨

var b : Character = "d"
var a : String = b // error


추가 데이터 타입
Any : Swift 의 모든 타입을 지칭하는 키워드
단, 
var some : Any = 100
var some2 : Double = some // error

AnyObject : 모든 클래스 타입을 지칭하는 프로토콜
nil : 없음(null)
단, Any에 nil 못 넣음


컬렉션 타입
Array : 순서가 있는 리스트 컬렉션
var array : Array<Int> = Array<Int>()
var array : Array<Int> = [Int]()
var array : [Int] = [Int]()
var array : [Int] = []
let array = [1, 2, 3] // 미리 멤버 정해서 생성도 가능, let 을 사용하면 아래의 메소드 사용 불가(변경이 안되는 뱅려이 됨)

array.append(1) > 맨 뒤에 1 삽입
contains(n) > n이 있는지 Bool
remove(i) > i번째 인덱스의 멤버 삭제
removeLast() > 마지막 멤버 삭제
removeAll() > 모두 삭제

Dictionary : 키와 값의 쌍으로 이루어진 컬렉션
var any : Dictionary<String, Any> = [String : Any]()
var any : [String, Any] = [:]
let .... // 변경 불가
var any : [String, Any] = ["d" : "d"]

Set : 순서가 없고, 멤버가 유일한 컬렉션
var some = Set<Int> = Set<Int>() // 축약문 없음
some.insert(n) // n값 삽입
contains(n)
remove(n)
removeFirst()
count // 크기


함수 기본
func 함수이름(매개변수1: 매개변수1타입, ....) -> 반환타입 {
	// body
	return 반환값
}

func .... -> Void {}

func 이름(매개 : 매개 타입 ...) {
	return 반환값 // 없을 수도 있음
} // 반환값 생략가능


함수 고급(advanced)
매개변수 기본값 : 함수의 매개변수에 값이 안들어와도 자동으로 값이 들어오는 것
func 함수이름(매개변수1 : 타입, 매개변수2 : 타입 = 값) -> 반환타입 {}
매개변수의 맨 뒤에 위치하는게 좋음

전달인자 레이블
전달인자 레이블은 함수를 호출할 때 매개변수의 역할을 좀 더 명확하게 하거나 함수 사용자의 입장에서 표현하고자 할 떄 사용

func 함수이름(전달인자1 매개변수1 : 타입, 전달인자 2매개변수2 : 타입 ... ) -> 반환타입 {}
함수이름(전달인자1 : 값, 전달인자2 : 값)

_  사용시 파마미터 안뜸


가변 매개변수
전달 받을 값의 개수르 ㄹ알기 어려울 떄 사용, 가변 매개변수를 함수당 하나만 가질 수 있음
func 함수이름(전달인자1 매개변수1 : 타입, 전달인자 2매개변수2 : 타입...) -> 반환타입 {}
... 을 이용하여 작성
몇개가 들어와도 상관없다는 뜻


스위프트는 함수형 프로그래밍 패러다임을 포함하는 다중 패러다임 언어
스위프트의 함수는 일급객체로 변수, 상수 등에 저장이 가능
매개변수를 통해 전달도 가능
함수는 하나의 데이터 타입으로도 사용 가능

(매개변수1타입, 매개2타입) -> 반환타입

var someFunc : (String, String) -> Void
someFunc = 함수("ㅇ", "ㅁ")

타입이 다른 함수는 할당 불가능(가변 매개변수도 타입이 다르다고 판단)


조건문
if else swich

if 조건
() 생략가능
{} 생략 불가능
Bool 타입만 조건문에 가능

switch value {
case pattern:
code
default:
code
}
범위 연산자
case 1..<100 : 1 이상 100 미만라는 의미>

case 1...100 : 1부터 100이하

value에는 대부분의 기본 타입사용가능

명시적으로 break 안해줘도 걸림
case pattern1, pattern2
또는
case pattern1
fallthrough
case pattern2

반복문
c 스타일 안됨
for item in items {
code
}
for each 와 유사
for i in 0...10 {}

dictionary는 튜플 타입으로 명시
for(name, age) in people {
code
}

while 조건 {
}
() 생략가능
Bool 만 조건으로

repeat-while
do-while과 동일


옵셔널
값이 있을 수도 없을 수도 있는 것을 표현
nil 의 가능성을 명시적으로 표현하기 위해 사용
전달 받은 값이 옵셔널이 아니면 nil 체크 안해도 됨 > 효율적, 안심, 든든


enum + general

enum Optional<Wrapped> : ExperssibleByNilLiteral {
case none
case some(Wrapped)
}

let foo: Optional<Int> = nil
let foo: Int? = nil // 축약가능

암시적 추출 옵셔널(Implicitly Unwrapped Optional) : !

var foo: Int! = 100

기존 변수처럼 사용가능
foo = foo + 1
nil 할당 가능
foo = nil
잘못된 접근시 런타임 에러


? optional : 일반적인 옵셔널
nil 할당 가능
기존 변수처럼 사용 불가능
foo = foo + 1 // error


옵셔널 값 추출
2가지 방법
optional binding
nil 체크 + 안전한 값 추출

func printName(_ name: String) {
print(name)
}
var myName: String? = nil
printName(myName) // error, 타입이 다름

if-let을 통해 옵셔널 바인딩 가능
if let name: String = myName {
printName(name)
} else {
}

printName(name) // name은 if-let 구문 안에서만 사용 가능, error

동시에 여러 옵셔널 바인딩 가능
if let name = myName, let friend = yourFreind {
print(...)
}


Force unwrapping(강제 추출)
var myName: String? = "d"
printName(myName!)

런타임 오류 발생할 위험 있음(값이 nil일 경우)
암시적 추출 옵셔널 타입은 강제 추출을 고려하고 설계함
즉
var name: String! = nil
printName(name) // ! 없어도 사용가능, 단 nil이 있기때문에 에러


구조체
값타입
상속 안됨
struct 이름 {
구현부
}

struct Sample {
var foo1: Int = 100 // 가변 프로퍼티
let ... // 불변

func method() {
} // 인스턴스 메소드

static method() {
} // 타입 메소드
}

var mutable: Sample = Sample() // 가변 인스턴스

let mutable: Sample = Sample() // 불변 인스턴스(가변 프로퍼티도 변경 불가능)


클래스
참조타입
다중상속 안됨

class 이름 {
구현부
}

static 메소드 // 상속 불가능
class 메소드 // 타입 메소드이지만 상속 가능


열거형 enum
enum은 값타입
소문자 카멜케이스로 정의
각 case느 ㄴ그 자체가 고유의 값

enum 이름 {
case 이름1 // 한줄씩 가능
case 이름2
case 이름 3, 이름,4 // 열거해도 됨
}

var day: Weekday = Weekday.mon
day = .tue // 타입이 확실하다면 축약가능

원시값(raw value)
enum도 정수값을 가질 수 있음
enum Fruit: Int {
case apple = 0
case grape = 1
case banana // 3
} // 자동으로 1씩 증가

문자열도 원시값으로 넣을 수 있음
School.이름1.rawValue //접근

원시값을 통한 초기화
rawValue를 통해 초기화 가능
rawValue가 case에 해당하지 않을 수 있으므로
rawValue를 통해 초기화한 인스턴스는 옵셔널 타입

let apple: Fruit = Fruit(rawValue: 0) // error
let apple: Fruit? = Fruit(rawValue: 0)

메서드로 enum에 추가가능

enum Sample {
case a
case b

func printmethod() {
switch self {
case .a
print("a")
default
print("b")
}
}
}

Sample.a.printmethod() // a
Sample.b.printmethod() // b



값 타입/ 참조(reference) 타입

구조체는 언제 사용하나?
연관된 몇몇의 값들을 모아서 하나의 데이터타입으로 표현할때
다른 객체 또는 함수 등으로 전달될 때 참조가 아닌 복사르 ㄹ원할때
자신을 상속할 필요 없거나 다른 타입을 상속받을 필요가 없을 때

값타입
데이터를 전달할 때 값을 복삭함

참조타입
메모리 위치를 전달함

스위프트의 데이터 타입은 구조체
int, double, string, dictionary, array, set


클로저
코드의 블록
일급 시민(first-citizen)
변수 상수드응로 저장 전달인자로 사용가능
함수 : 일므이 있는 클로저

{ (매개변수 목록) -> 반환타입 in
실행코드
}

클로저 고급
다양한 표현이 가능하기에 이해하기 쉽게 적는게 중요

후행 클로저
// 이따가 적자



프로퍼티
종류
저장 프로퍼티
연산

역할
인스턴스
타입

struct A {
var foo: Int {
get {
return 반환값
}
set(매개변수) {
연산내용
}
}
} // 연산 프로퍼티

set에 매개변수 작성안하면 암시적 매개변수 newValue로 사용가능


프로퍼티 감시자
프로퍼티 값의 변경될 때 원하는 동작을 수행

willSet(매개변수 // 바뀔 값) {
} // 바뀌기 직전

didSet(매개변수 // 바뀌기 이전 값) {

} // 바뀐 후

매개변수는 암시적 매개변수 newValue, oldValue 사용 가능

연산 프로퍼티 안에는 프로퍼티 감시자 사용 불가




상속
class 만 가능
class 이름: 부모 {

}
저장 프로퍼티 재정의 불가
final 키워드 : 오버라이드 불가
final class : 재정의 불가


인스턴스 생성과 소멸
init, deinit
오버로딩 가능
convenience

init 에도 옵셔널 가능
return nil의 경우 인스턴스 생성 안함
단, init 이 옵셔널이면 타입도 옵셔널로 선언

deinit
클래스타입에만 가능


옵셔널 체이닝과 nil 병합 연산자
옵셔널 체이닝 : 연속적으로 옵셔널 값 추출
옵셔널 요소 내부의 프로퍼티로 또다시 옵셔널이 연속적으로 연결도는 경우 유용

if let 을 연속적으로 사용해야하는 경우
foo?.foo1?.foo2 로 옵셔널 체이닝 가능

값이 없으며 ㄴnil 리턴


nil 병합 연산자
?? : 플루터랑 동일


타입 케스팅
is, as 사용

is 를 이용하여 타입 화깅ㄴ 가능 interfaceof랑 동일
값 is 타입 // 값 == 타입인지 확인 Bool

switch 문에도 사용 가능

업캐스팅
as를 이용하여 타입 케스팅 가능
암시적으로 생략됨

다운캐스팅
as?, as!를 사용
as? 조건부 다운캐스팅, 실패되면 nil 반환
as! 강제 다운캐스팅, 실패하면 ㅈ됨


assert 와 guard
assert는 디버깅 모드에서만 작동
assert(조건, 실패했을 때 메시지)
조건이 true이면 넘어감

guard
Early exit을 위한 문법, return, break 와 같은 종료문법을 반드시 사용해야함
guard는 디버깅 뿐만 아니라 전 부분 사용가능

gaurd 조건들... else {
조건 실패 문
return 또는 break 반드시 명시
}
조건에 선언된 프로퍼티는 guard 구문을 넘어서도 사용 가능
타입 캐스팅에서 많이 사용하며 딕셔너리 구조에서도 많이 사용


프로토콜
특정 역할을 수행하기 위한 메서드, 프로퍼티, 이니셜라이저 등의 요구사항을 정의
구조체, 클래스, 열거형은 모두 프로토콜을 채택(Adopted)해서 요구사하을 구현할 수 있음
프로토콜의 요구샇아ㅡㄹ 모두 따르는 타입은 그 프로포콜을 준수(Conform)한다 라고 함
프로토콜을 준수하려면 해당 프로토콜이 요구하는 요구사항을 모두 구현해야 함

인터페이스라고 생각하면 됨

protocol 프로토콜이름 {
요구사항
}

프로토콜 상속 : 다중상속 가능
protocol 이름 : 프로토콜들... {}

클래스에서 프로토콜 상속
class 이름 : 부모클래스, 프로토콜들.... {
} // 순서 중요




