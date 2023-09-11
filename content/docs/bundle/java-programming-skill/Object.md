# Object

Object 클래스는 모든 클래스의 최고 조상으로 `java.lang` 패키지에 포함되어 있습니다.

Object 클래스는 필드는 없고 메소드만 가지고 있습니다. 이러한 멤버들은 모든 클래스에서 바로 사용 가능합니다.

## Object 클래스의 구조

Object는 모든 클래스들에 상속되며, 필요에 따라 오버라이드하여 사용합니다.
이러한 Object 클래스의 구조는 아래와 같습니다.

```java
package java.lang;  
  
import jdk.internal.vm.annotation.IntrinsicCandidate;  
  
public class Object {  
  
    public Object() {}  
  
    public final native Class<?> getClass();  
  
    @IntrinsicCandidate
    public native int hashCode();  
  
    public boolean equals(Object obj) {  
        return (this == obj);  
    }  
    
    @IntrinsicCandidate
    protected native Object clone() throws CloneNotSupportedException;
    
	public String toString() {  
        return getClass().getName() + "@" + Integer.toHexString(hashCode());
    }  
    
    public final native void notify();  
  
    public final native void notifyAll();  
    
    public final void wait(long timeoutMillis, int nanos) throws InterruptedException {  
        if (timeoutMillis < 0) {  
            throw new IllegalArgumentException("timeoutMillis value is negative");  
        }  
        if (nanos < 0 || nanos > 999999) {  
            throw new IllegalArgumentException(  
                                "nanosecond timeout value out of range");  
        }  
        if (nanos > 0 && timeoutMillis < Long.MAX_VALUE) {  
            timeoutMillis++;  
        }  
        wait(timeoutMillis);  
    }
    
    protected void finalize() throws Throwable { }  
}
```

- `@IntrinsicCandidate` : HotSpot VM (현재 대다수 JVM) 에 의해 최적화하겠다는 의미로서, 작성된 코드를 보다 효율적인 내부적 동작으로 덮어쓰게 됩니다.

- `native` : Java Native Interface를 사용하여 C, C++ 등 다른 언어로 작성된 코드를 호출하겠다는 의미로 성능 향상을 위해 사용합니다.

### toString 메소드
기본적으로 toString() 은 해당 클래스 정보(이름)를 가지는 getName() 과 해당 해시코드를 반환하게 됩니다.

```java
public String toString() {  
    return getClass().getName() + "@" + Integer.toHexString(hashCode());  
}
```

모든 클래스는 Object를 부모 클래스로 가지기 때문에 toString 메서드를 오버라이드하여 개조하여 사용할 수 있습니다.

### 