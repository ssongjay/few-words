# Thread Local

## 스레드 로컬이란?
인스턴스의 필드에 접근하면 원래 저장되어있던 데이터는 후에 접근한 다른 스레드에 의해서 덮어 씌워질 수 있다
이 상황에서 최초에 접근했던 A스레드가 다시 필드에 접근했을 때 원래 데이터를 찾을 수 없게 된다.

이를 해결하기 위해 스레드 로컬을 사용한다. 스레드 로컬은 스레드별로 독립적인 저장 공간을 제공하여 해당 스레드에서만 접근할 수 있도록하여
 각 스레드가 독립적인 값을 가질 수 있게 된다.

## 스레드 로컬 사용법
스레드 로컬은 ThreadLocal 클래스를 사용하여 구현한다. ThreadLocal 클래스는 제네릭 클래스로 선언되어 있어서 저장하고자 하는 데이터의 타입을 명시해야 한다.

```java
public class ThreadLocalExample {
    public static void main(String[] args) {
        ThreadLocal<String> threadLocal = new ThreadLocal<>();
        threadLocal.set("Hello, World!");
        System.out.println(threadLocal.get());
    }
}
```

위 코드는 ThreadLocal 클래스를 사용하여 스레드 로컬을 구현한 예제이다. ThreadLocal 클래스는 set() 메서드를 사용하여 데이터를 저장하고 get() 메서드를 사용하여 데이터를 조회한다.

## 스레드 로컬 사용 시 주의사항
스레드 로컬을 사용할 때 주의해야 할 점은 메모리 누수이다. 스레드 로컬은 스레드별로 독립적인 저장 공간을 제공하기 때문에
스레드가 종료되어도 데이터가 메모리에 남아있을 수 있다. 그렇지 않을 경우 재사용 되는 스레드가 잘못된 데이터를 참조하는 상황이 생길 수 있다. 
이를 방지하기 위해 스레드가 종료될 때 데이터를 삭제하는 작업이 필요하다.


```java
public class ThreadLocalExample {
    public static void main(String[] args) {
        ThreadLocal<String> threadLocal = new ThreadLocal<>();
        threadLocal.set("Hello, World!");
        System.out.println(threadLocal.get());
        threadLocal.remove();
    }
}
```

위 코드는 스레드 로컬에 저장된 데이터를 삭제하는 방법을 보여준다. remove() 메서드를 사용하여 데이터를 삭제할 수 있다.

