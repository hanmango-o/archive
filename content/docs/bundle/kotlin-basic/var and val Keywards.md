---
showToc: true
---

# var and val Keywards
변수는 값을 담는 컨테이너입니다. Kotlin에서 변수를 생성하는 방법에 대해 알아봅니다.

----

## 2가지 방법 : `var` or  `val`
Kotlin에서의 변수 생성은 `var` 와 `val` 키워드를 사용하는 2가지 방법이 있습니다.

### var keyword
`var` 는 변경이 가능한 변수(mutable)를 생성할 때 사용하는 키워드입니다.

```kotlin
fun main() {  
    var name = "HAN"  
    print("Hello $name") // Hello HAN  
}
```

해당 키워드로 선언된 변수는 아래와 같이 변경이 가능합니다.

```kotlin
fun main() {  
    var name = "HAN"  
    name = "Kotlin" // Can change value  
    print("Hello $name") // Hello Kotlin  
}
```


### val keyword
`val` 는 한번 할당되면 변경이 불가능한 변수(immutable)를 생성할 때 사용하는 키워드입니다.

```kotlin
fun main() {  
    val name = "HAN"  
    print("Hello $name") // Hello HAN  
}
```

해당 키워드로 선언된 변수는 아래와 같이 변경이 불가능합니다.

```kotlin
fun main() {  
    val name = "HAN"  
    name = "Kotlin" // ERROR:Val cannot be reassigned  
    print("Hello $name") // Hello Kotlin  
}
```


> [!Tip]
> Kotlin 공식 레퍼런스에서는 val 사용을 권장합니다.

----

## Type annotation & initialized
아래와 같이 변수 선언 이후 initailize 하는 경우 컴파일 에러가 발생합니다.

```Kotlin
fun main() {  
    // ERROR:This variable must either have a type annotation or be initialized  
    val name  
    name = "Kotlin"   
	print("Hello $name")  
}
```

이는 해당 변수의 return type 이 명시되어 있지 않아 발생하는 에러입니다.

Kotlin에서 모든 변수는 생성과 동시에 initialize 되거나, type annotation을 가지고 있어야 합니다.

### Type annotation
type annotation은 String, Int 와 같은 해당 변수의 타입을 의미합니다.

Kotlin에서는 아래와 같이 명시합니다.

```Kotlin
fun main() {
    val name: String  
    name = "Kotlin"  
	print("Hello $name")  
}
```

상단의 코드는 선언과 동시에 initialize 해도 무방합니다. 이는 아래와 같습니다.

```Kotlin
fun main() {
    val name: String = "Kotlin"
	print("Hello $name")  
}
```

단, 해당 경우 할당된 값이 String 이기 때문에 컴파일러가 초기화된 값에 맞춰 type annotation을 할당해줍니다.

따라서 아래와 같이 수정할 수 있습니다.

```Kotlin
fun main() {
    val name = "Kotlin"
	print("Hello $name")  
}
```

----
**Summary :**
- Kotlin의 변수 생성 방법에는 var(변경이 가능한 변수)와 val(변경이 불가능한 변수)가 있다.
- 모든 변수는 initialized 되거나 type annotation을 명시해야 한다.

**Links :**
- https://www.udemy.com/course/kotling-android-jetpack-compose-/