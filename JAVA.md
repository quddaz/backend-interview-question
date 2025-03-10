# JAVA 

<details>
  <summary><h3>1. JVM의 구조와 Java의 실행방식이 뭔가요?</h3></summary>
JVM (Java Virtual Machine) 은 자바 애플리케이션을 실행하는 가상 머신으로, 클래스 로딩, 실행, 메모리 관리 등을 담당합니다.

> ✔ JVM의 구조

<li>클래스 로더: 바이트코드를 JVM으로 로드
<li>실행 엔진: 바이트코드 실행 (인터프리터 & JIT 컴파일러)
<li>메모리 영역: 스택(지역 변수), 힙(객체 저장), 메소드 영역(클래스 정보)

> ✔ Java 실행 방식

<li>자바 코드를 컴파일러가 바이트코드로 변환
<li>클래스 로더가 JVM에 로드
<li>실행 엔진이 바이트코드를 해석 & 실행
  
즉, "컴파일 → 로드 → 실행"의 과정으로 동작합니다.
</details>

<details>
  <summary><h3>2. Call by value와 Call by Reference에 대해 설명해주세요.</h3></summary>
  
> Call by value
  
```
  void func(int n) {
    n = 20;
}

void main() {
    int n = 10;
    func(n);
    printf("%d", n);
}
```
Call by value는 함수의 매개변수로 값을 복사해서 전달합니다.
이때 복사된 인자는 함수 안에서 지역적으로 사용되기에 local value 속성을 가집니다.

> Call by reference

```
void func(int *n) {
    *n = 20;
}

void main() {
    int n = 10;
    func(&n);
    printf("%d", n);
}
```
Call by reference는 함수의 매개변수로 래퍼런스를 전달합니다. 그래서 함수 안에서 해당 값이 변경되면 전달된 객체의 값도 변경됩니다. 

물론 JAVA는 기본적으로 모든 함수가 Call by value 형태로 사용되며 객체의 경우는 참조(주소 값)을 복사하여 객체 내부의 값을 변경할 수 있습니다. 
</details>

<details>
  <summary><h3>3. Primitive type & Reference type에 대해 설명해주세요</h3></summary>

> 자바의 타입

자바는 기본형과 참조형 타입이 있습니다. 

> Primitive type (기본형 타입)
- 자바는 총 8가지의 기본형 타입을 제공합니다.
- 비객체 타입이며 따라서 null 타입을 가질 수 없습니다. 만약 필요하다면 래퍼 클래스를 사용해야합니다.
- 스택 메모리에 저장됩니다.
     - boolean : 논리형 타입이며 참/거짓으로 저장합니다. 1byte의 형태입니다.
     - byte : 주로 이진데이터를 다루는 타입입니다.
     - short : c와의 호환을 위해 사용되는 타입이지만 잘 사용하지 않습니다.
     - int
     - long
     - float, double : 실수를 부동소수점 방식으로 저장합니다.
  
> Reference type (참조형 타입)
- JAVA에서 기본형 타입을 제외한 모든 타입이 참조형 타입입니다.
- 해당 타입은 JAVA의 Object 클래스를 상속하는 모든 클래스를 말합니다.
- 메모리 영역인 힙 메모리에 저장됩니다.
- 빈 객체를 의미하는 null이 존재합니다. 
    - 클래스 타입
    - 인터페이스 타입
    - 배열 타입
    - 열거 타입
> String Class

자바의 String 클래스는 조금 특별합니다. 기본적인 사용은 기본형처럼 사용하지만 불변하는 객체입니다. 그렇기에 String을 변경하면 갱신이 아닌 새로운 값을 반환합니다. 
String 객체간의 비교는 .equals를 사용합니다. 
</details>

<details>
  <summary><h3>4. Wrapper Class가 무엇인가요?</h3></summary>

자바에는 기본 타입(Primitive Type)과 이를 감싸는 **Wrapper 클래스**가 존재합니다.  
Wrapper 클래스는 기본 타입을 객체로 다룰 수 있도록 제공되는 클래스입니다.

### ✅ 기본 타입 vs Wrapper 클래스
- **기본 타입(Primitive Type)**: `int`, `long`, `float`, `double`, `boolean`, `char`, `byte`, `short`
- **Wrapper 클래스**: `Integer`, `Long`, `Float`, `Double`, `Boolean`, `Character`, `Byte`, `Short`

---

## 🎯 **Wrapper 클래스의 주요 기능**
### 1️⃣ **기본 타입을 객체로 변환 (Boxing, Unboxing)**
```java
int num = 10;
Integer obj = Integer.valueOf(num); // Boxing (기본 타입 → 객체)
int value = obj.intValue(); // Unboxing (객체 → 기본 타입)
```
### 2️⃣ **자동 변환(Auto Boxing, Auto Unboxing)**
```
Integer num = 10; // Auto Boxing (int → Integer)
int value = num;  // Auto Unboxing (Integer → int)
```

### 3️⃣ **Wrapper 클래스의 비교 (주의점!)**
```java
Integer a = 1000;
Integer b = 1000;
System.out.println(a == b);  // false (주소값 비교)

int c = 1000;
int d = 1000;
System.out.println(c == d);  // true (값 비교)
```
- Wrapper 클래스는 주소 값을 비교하므로 equals()를 이용해서 값을 비교해야합니다. 

### 🚀 Wrapper 클래스의 성능 고려 사항
- Wrapper 클래스는 기본 타입보다 메모리 사용량이 많습니다. 
- 그렇기에 섣부른 사용은 피하는 것이 좋습니다.
</details>

<details>
  <summary><h3>5. 직렬화는 무엇이고 java에서는 왜 사용하나요?</h3></summary>

## ✅ 직렬화(Serialization)란?
- **직렬화**는 객체를 **바이트 스트림**으로 변환하여 **파일**이나 **네트워크**를 통해 전달할 수 있게 만드는 과정입니다.
- **역직렬화(Deserialization)**는 직렬화된 바이트 스트림을 다시 객체로 변환하는 과정입니다.

### 📌 직렬화의 필요성
- **파일 저장**: 객체를 파일로 저장하고, 나중에 다시 복원하려면 직렬화와 역직렬화가 필요합니다.
- **네트워크 통신**: 네트워크를 통해 객체를 전달할 때 객체를 바이트 형식으로 전송해야 하기 때문에 직렬화가 필요합니다.
- **분산 시스템**: 객체를 서로 다른 시스템 간에 전달할 때 직렬화가 필수적입니다.

---

## 🎯 자바에서 직렬화 사용 이유
1. **네트워크 전송**  
   객체를 네트워크를 통해 전송할 때, 자바는 객체를 바이트 형식으로 변환하여 데이터를 전송할 수 있습니다. 이때 직렬화가 사용됩니다.

2. **세션 저장**  
   웹 애플리케이션에서 사용자의 세션 정보를 저장할 때 객체를 직렬화하여 세션에 저장하거나, 파일 시스템에 저장할 수 있습니다.

3. **클러스터링 및 분산 처리**  
   여러 서버 간에 객체를 주고 받을 때 직렬화가 필요합니다. 예를 들어, 클러스터링된 환경에서는 객체를 네트워크를 통해 다른 서버로 전송해야 할 때 직렬화가 사용됩니다.

4. **파일 시스템 저장**  
   객체를 파일 시스템에 저장할 때 직렬화를 통해 객체를 바이트 스트림으로 변환한 후 저장하고, 나중에 역직렬화하여 객체를 복원합니다.

---

## 🎯 자바에서 직렬화 구현 방법
- 자바에서 **직렬화**를 구현하려면 `java.io.Serializable` 인터페이스를 구현해야 합니다.

### ✅ 직렬화 예제
```java
import java.io.*;

class Person implements Serializable {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }
}

public class SerializationExample {
    public static void main(String[] args) {
        try {
            // 객체 직렬화
            Person person = new Person("John", 30);
            ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("person.ser"));
            out.writeObject(person);
            out.close();

            // 객체 역직렬화
            ObjectInputStream in = new ObjectInputStream(new FileInputStream("person.ser"));
            Person deserializedPerson = (Person) in.readObject();
            in.close();

            System.out.println("Deserialized Person: " + deserializedPerson);
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```
### 🎯 **직렬화와 관련된 고려 사항**
- transient 키워드
직렬화할 때 특정 필드를 제외하고 싶다면 해당 필드에 transient 키워드를 붙일 수 있습니다. 이는 해당 필드를 직렬화하지 않겠다는 의미입니다.

### 🎯 결론
직렬화는 객체를 바이트 스트림 형태로 변환하여 저장하거나 전송하는 기술입니다. 이 기술은 객체 자체를 메모리 주소로 전달하므로 Reference Type의 타입의 데이터들은 다른 OS나 환경에서는 전달이 불가능합니다. 그렇기에 만들어진 기술입니다. 

</details>

<details>
  <summary><h3>6. 문자열 클래스와 StringBuffer, StringBuilder 특징</h3></summary>

## 📌 **String 클래스**
- **불변(Immutable) 클래스**입니다.
- **문자열의 변경** 시 새로운 객체가 생성됩니다.
- 이로 인해 **성능이 저하**될 수 있으며, 문자열을 자주 변경할 경우 `StringBuilder` 또는 `StringBuffer`를 사용하는 것이 더 효율적입니다.
- 문자열 비교 시 `==` 연산자를 사용할 수 있지만, **문자열 내용 비교**는 `.equals()` 메서드를 사용해야 합니다.
- 예:
 ```java
  String s1 = "hello";
  String s2 = "hello";
  System.out.println(s1 == s2);      // true (같은 리터럴을 가리킴)
  System.out.println(s1.equals(s2)); // true (값이 동일)
```

## 📌 **StringBuffer 클래스**
- 가변 문자열 클래스입니다.
- 멀티스레드 환경에서 안전하게 사용할 수 있습니다. (스레드 동기화 처리가 자체적으로 되어있습니다.)
- 문자열 변경 작업을 수행할 때, 새로운 객체를 생성하지 않고 기존 버퍼에서 수정합니다.
- 성능상 StringBuilder보다 느리지만, 멀티스레드 환경에서 더 적합합니다.

## 📌 **StringBuffer 클래스**
- 가변 문자열 클래스입니다.
- StringBuffer와 비슷하지만, 멀티스레드 환경에서는 안전하지 않습니다.
- 문자열을 자주 변경해야 할 때 더 효율적이며, StringBuffer보다 빠릅니다.
- 멀티스레드가 아닌 환경에서 성능이 더 우수합니다.

## 🎯 **결론**
- String은 불변 객체로, 문자열이 자주 변경되면 성능에 영향을 미칠 수 있습니다.
- StringBuffer는 멀티스레드 환경에서 안전하지만, 성능은 StringBuilder보다 떨어집니다.
- StringBuilder는 멀티스레드 환경을 고려하지 않는 비멀티스레드 환경에서 가장 성능이 뛰어납니다.
  
</details>

<details>
  <summary><h3>7. Casting(업캐스팅 & 다운캐스팅)의 필요성에 대해 설명하세요.</h3></summary>

## 📌 **업캐스팅 (Upcasting)**
- **자식 클래스** 타입을 **부모 클래스** 타입으로 변환하는 과정입니다.
- 자식 클래스는 부모 클래스의 특성을 **상속** 받으므로, 자식 클래스의 객체를 부모 클래스 타입으로 변환할 수 있습니다.
- 업캐스팅은 **자동으로** 이루어지며, 별도의 연산자가 필요하지 않습니다.
- **다형성(polymorphism)** 을 활용하여, 부모 클래스 타입으로 자식 클래스 객체를 다룰 수 있습니다.

### 예시:
```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal = new Dog(); // 업캐스팅
        animal.sound(); // "Dog barks" 출력
    }
}
```
- 여기서 `Dog` 객체는 `Animal` 타입으로 업캐스팅되어, 부모 클래스 `Animal`의 참조 변수로 다뤄집니다.
- **다형성**을 이용하여, 부모 클래스의 메서드를 자식 클래스의 구현으로 호출할 수 있습니다.

---

## 📌 **다운캐스팅 (Downcasting)**
- **부모 클래스** 타입을 **자식 클래스** 타입으로 변환하는 과정입니다.
- 다운캐스팅은 **명시적**으로 해야 하며, 잘못된 형변환이 발생할 수 있기 때문에 **주의**가 필요합니다.
- **ClassCastException**이 발생할 수 있기 때문에, 안전하게 타입 변환을 하려면 **instanceof**를 사용하여 확인하는 것이 좋습니다.

### 예시:
```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal = new Dog();  // 업캐스팅
        Dog dog = (Dog) animal;     // 다운캐스팅
        dog.sound(); // "Dog barks" 출력
    }
}
```
- 위의 예시에서, `animal` 객체는 `Animal` 타입이지만, `Dog` 객체이므로 다운캐스팅을 통해 다시 `Dog` 타입으로 변환합니다.

### 주의점:
- 다운캐스팅을 할 때는 반드시 **실제 객체가 해당 타입인지** 확인해야 합니다. 그렇지 않으면 **ClassCastException**이 발생할 수 있습니다.
- `instanceof` 연산자를 사용하여 타입이 맞는지 확인한 후, 다운캐스팅을 수행하는 것이 안전합니다.

```java
if (animal instanceof Dog) {
    Dog dog = (Dog) animal;  // 안전한 다운캐스팅
    dog.sound();
}
```

---

## 🎯 **업캐스팅과 다운캐스팅의 필요성**
- **업캐스팅**은 다형성을 이용해 **부모 클래스 타입으로 자식 객체를 처리**할 수 있어, 코드의 유연성을 높이고, 부모 클래스의 공통 메서드를 사용하도록 합니다.
- **다운캐스팅**은 실제 객체의 구체적인 클래스에 접근해야 할 때 필요합니다. 예를 들어, 부모 클래스에서 정의되지 않은 자식 클래스의 특화된 메서드를 사용하고자 할 때 다운캐스팅이 필요합니다.

### **업캐스팅과 다운캐스팅의 용도**
- **업캐스팅**: 부모 클래스 타입의 변수로 자식 클래스 객체를 다룰 때 사용.
- **다운캐스팅**: 부모 클래스 타입의 변수에서 자식 클래스 타입으로 변환하여 자식 클래스에만 있는 특화된 기능을 사용할 때 사용.

스프링에서는 **서비스 인터페이스** 와 **구현 클래스**의 관계에서 업캐스팅을 주로 사용합니다.
</details>

<details>
  <summary><h3>8. Thread에 대해 설명하세요.</h3></summary>

현대의 운영체제는 **멀티태스킹**을 지원합니다. 멀티태스킹이란, 한정된 CPU의 코어 개수로 실제로 동시에 처리되는 것처럼 번갈아가며 여러 작업을 수행하는 방식입니다. 이처럼 **멀티스레딩**은 하나의 **프로세스** 안에서 여러 개의 **스레드**가 동시에 작업을 수행하는 것입니다.

---

### 🎯 **스레드(Thread)**

- **스레드**는 프로세스 내에서 실행되는 **가벼운 실행 단위**입니다.
- 각 스레드는 **프로세스의 주소 공간**을 공유하며, **메모리와 리소스를 공유**하기 때문에 스레드 간의 **통신**이 용이합니다.
- 스레드는 **CPU 코어**에서 작업을 수행하는 가장 작은 단위로, 여러 스레드가 동시에 실행되는 것처럼 보이는 **멀티태스킹**을 가능하게 합니다.

### 📌 **스레드의 특징**

1. **멀티스레딩**: 하나의 프로세스가 여러 스레드를 포함할 수 있으며, 이 스레드들이 동시에 실행됩니다.
2. **경량 프로세스**: 스레드는 프로세스보다 **작고 가벼운** 실행 단위로, 프로세스보다 생성 및 관리가 더 효율적입니다.
3. **자원 공유**: 스레드들은 동일한 메모리 공간을 공유하므로, 다른 스레드와 빠르고 쉽게 **데이터를 공유**할 수 있습니다.
4. **병렬 처리**: 여러 스레드를 사용하여 **병렬 처리**를 통해 처리 성능을 향상시킬 수 있습니다.

### 🎯 **자바에서의 스레드 사용**

자바에서는 `Thread` 클래스를 사용하거나 `Runnable` 인터페이스를 구현하여 스레드를 생성할 수 있습니다. 이를 통해 멀티스레딩 환경에서 여러 작업을 동시에 처리할 수 있습니다.

#### 1. **Thread 클래스 사용하기**
`Thread` 클래스를 상속받아서 스레드를 생성합니다.

```java
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Thread is running");
    }
}

public class ThreadExample {
    public static void main(String[] args) {
        MyThread thread = new MyThread();
        thread.start();  // 스레드 실행
    }
}
```

#### 2. **Runnable 인터페이스 사용하기**
`Runnable` 인터페이스를 구현하여 스레드를 실행할 수 있습니다. 이 방법은 여러 스레드 작업을 동시에 실행할 때 유용합니다.

```java
class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Runnable thread is running");
    }
}

public class RunnableExample {
    public static void main(String[] args) {
        MyRunnable runnable = new MyRunnable();
        Thread thread = new Thread(runnable);
        thread.start();  // 스레드 실행
    }
}
```

### 🎯 **스레드의 상태**
스레드는 여러 상태를 가질 수 있습니다:
- **New**: 생성된 스레드가 아직 시작되지 않은 상태
- **Runnable**: 스레드가 실행을 준비하고, CPU가 스레드를 실행 중인 상태
- **Blocked**: 다른 스레드의 리소스를 기다리는 상태
- **Waiting**: 다른 스레드의 작업이 끝날 때까지 대기 중인 상태
- **Terminated**: 스레드가 종료된 상태

### 🎯 **스레드 동기화**
멀티스레딩 환경에서는 여러 스레드가 동시에 공유 자원을 수정할 수 있기 때문에 **데이터 경합**(race condition)이 발생할 수 있습니다. 이를 방지하기 위해 **동기화(synchronization)** 가 필요합니다.

```java
class Counter {
    private int count = 0;

    public synchronized void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}

public class SyncExample {
    public static void main(String[] args) {
        Counter counter = new Counter();
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        });

        t1.start();
        t2.start();
    }
}
```
위의 예제에서 `increment` 메서드에 `synchronized`를 사용하여 두 스레드가 동시에 `count` 값을 수정할 수 없도록 합니다.

### 🎯 **결론**
- 스레드는 프로세스 내에서 작업을 수행하는 실행 단위로, 멀티스레딩을 통해 동시에 여러 작업을 처리할 수 있습니다.
- 자바에서는 `Thread` 클래스나 `Runnable` 인터페이스를 사용하여 멀티스레드를 구현할 수 있습니다.
- **동기화**를 통해 여러 스레드가 안전하게 자원을 공유할 수 있도록 관리해야 합니다.

스레드의 이해와 활용은 멀티태스킹과 병렬 처리를 위한 핵심적인 기술입니다.
</details>

<details>
  <summary><h3>9. Garbage Collection에 대해 설명하세요.</h3></summary>

**Garbage Collection**(GC)은 자바에서 메모리 관리의 일환으로, **사용되지 않는 객체**를 자동으로 **제거**하는 프로세스입니다. 이는 개발자가 **메모리 누수**를 방지하고, 메모리를 효율적으로 관리할 수 있도록 도와줍니다. GC는 자바의 **JVM**(Java Virtual Machine)에서 자동으로 수행되며, 개발자는 직접 메모리를 해제할 필요가 없습니다.

---

### 🎯 **GC의 주요 역할**

- **자동 메모리 관리**: 객체가 더 이상 필요 없을 때 이를 자동으로 식별하고 메모리에서 제거하여, 개발자가 직접 메모리 관리에 신경 쓸 필요를 줄여줍니다.
- **메모리 누수 방지**: 객체가 더 이상 참조되지 않으면 이를 GC가 회수하여 **메모리 누수를 방지**합니다.
- **힙 메모리 최적화**: GC는 프로그램 실행 중에 발생하는 **메모리 할당과 해제**를 최적화하여, 사용 가능한 메모리를 효율적으로 관리합니다.

### 🎯 **Garbage Collection 동작 원리**

Garbage Collection은 주로 **힙 메모리**에서 이루어집니다. 자바에서 객체는 힙 영역에 저장되며, 이 객체들이 더 이상 참조되지 않으면 **GC**가 이를 회수합니다.

1. **참조되지 않는 객체 탐지**: GC는 더 이상 참조되지 않는 객체를 찾아 **쓰레기**로 간주하고 회수합니다.
2. **메모리 회수**: 불필요한 객체를 제거하여 사용 가능한 메모리를 확보합니다.
3. **자동 실행**: GC는 자바 애플리케이션이 실행되는 동안 자동으로 수행되며, 프로그래머가 명시적으로 호출할 필요가 없습니다.

### 🎯 **GC의 주요 단계**

1. **마크(mark)**: GC는 먼저 **마크(marking)** 단계를 수행하여, 현재 살아있는 객체들을 식별합니다. 살아있는 객체는 여전히 다른 객체나 스레드에서 참조되는 객체입니다.
2. **정리(sweep)**: 살아있는 객체를 제외한 나머지 객체들을 메모리에서 정리합니다. 이렇게 정리된 메모리 공간은 재사용될 수 있습니다.
3. **압축(compact)**: 메모리에서 빈 공간을 제거하고, 남은 객체들을 모아서 힙 메모리 내에서 연속된 공간을 만들기도 합니다. 이는 **단편화** 문제를 해결하기 위한 과정입니다.

### 🎯 **GC의 종류**

1. **Minor GC**: 
   - **Young Generation**에서 발생하며, 새로운 객체들이 할당되는 공간에서 발생합니다.
   - 짧은 시간 안에 빠르게 실행됩니다.
   - **Eden** 영역과 **Survivor** 영역에서 발생합니다.

2. **Major GC**: 
   - **Old Generation**에서 발생하며, 오랜 시간 살아남은 객체들이 모여있는 공간에서 발생합니다.
   - 상대적으로 더 긴 시간이 걸리고, 애플리케이션의 성능에 영향을 줄 수 있습니다.

3. **Full GC**: 
   - **Young Generation**과 **Old Generation** 모두를 대상으로 하는 GC입니다.
   - 가장 비용이 많이 드는 GC로, 시스템 성능에 영향을 미칠 수 있습니다.

### 🎯 **GC의 알고리즘**

1. **Serial GC**:
   - 단일 스레드를 사용하여 GC를 수행합니다.
   - 작은 애플리케이션이나 멀티코어 환경이 아닌 환경에서 사용됩니다.

2. **Parallel GC**:
   - 여러 스레드를 사용하여 GC를 병렬로 수행합니다.
   - 멀티코어 시스템에서 성능이 향상됩니다.

3. **Concurrent Mark-Sweep (CMS) GC**:
   - GC가 애플리케이션 실행과 동시에 **병렬**로 객체를 마킹하고 정리할 수 있도록 지원합니다.
   - 응답 속도가 중요한 애플리케이션에 유리합니다.

4. **G1 GC**:
   - 대규모 애플리케이션에 적합한 GC로, **리전** 단위로 메모리를 관리합니다.
   - **Low Pause Time**(짧은 일시 정지 시간)을 목표로 설계되었습니다.

### 🎯 **Garbage Collection의 장점과 단점**

#### 장점:
- **자동화된 메모리 관리**: 개발자가 메모리 관리에 신경 쓸 필요가 없으므로 편리합니다.
- **메모리 누수 방지**: 더 이상 사용되지 않는 객체를 자동으로 회수하여 메모리 누수를 방지합니다.
- **효율적인 자원 관리**: GC는 최적의 성능을 위해 메모리와 자원을 효율적으로 관리합니다.

#### 단점:
- **성능 저하**: GC가 실행되는 동안 애플리케이션의 실행이 잠시 멈출 수 있기 때문에 성능에 영향을 미칠 수 있습니다.
- **예측 불가능한 일시 정지**: GC가 언제 실행될지 예측할 수 없으므로, 대규모 시스템에서는 성능 예측이 어려울 수 있습니다.

### 🎯 **결론**

Garbage Collection은 자바 애플리케이션에서 메모리 관리를 자동으로 처리하는 중요한 기술입니다. 이를 통해 개발자는 메모리 해제를 직접 관리할 필요 없이, 안정적이고 효율적인 애플리케이션을 개발할 수 있습니다. 그러나 GC의 실행은 애플리케이션의 성능에 영향을 미칠 수 있으므로, GC의 종류와 특성을 이해하고 적절하게 활용하는 것이 중요합니다.
</details>

<details>
  <summary><h3>10. Error와 Exception</h3></summary> 

**Error**와 **Exception**은 자바에서 예외 처리에 사용되는 두 가지 주요 개념으로, 중요한 차이점이 있습니다.

### 1. **Error**
- **Error**는 시스템 수준에서 발생하는 심각한 문제로, 프로그램이 정상적으로 실행될 수 없을 정도로 시스템에 영향을 미칩니다.
- **대표적인 Error**:
  - `OutOfMemoryError`: JVM 힙 메모리가 부족하여 더 이상 객체를 할당할 수 없는 경우
  - `StackOverflowError`: 메서드 호출 스택이 넘칠 때 발생하는 오류
  - `VirtualMachineError`: JVM에 심각한 문제 발생

**특징**:
- **복구 불가능**: `Error`는 대부분 복구가 불가능한 상황에서 발생합니다. 예를 들어, 메모리 부족이나 스택 오버플로우와 같은 시스템 오류는 프로그램 자체에서 해결할 수 없습니다.
- **예외 처리 불필요**: 일반적으로 `Error`는 개발자가 처리하지 않아도 됩니다. 이는 시스템의 문제로, 프로그램의 논리적인 문제는 아니기 때문입니다.

### 2. **Exception**
- **Exception**은 프로그램 실행 중 예기치 않은 상태에서 발생하는 문제로, 시스템의 오류는 아니지만 프로그램의 정상적인 흐름을 방해합니다.
- **대표적인 Exception**:
  - `NullPointerException`: 객체가 `null`인 상태에서 메서드나 필드에 접근할 때 발생
  - `ArrayIndexOutOfBoundsException`: 배열의 인덱스를 초과하여 접근할 때 발생
  - `IOException`: 입출력 작업 중 발생하는 예외

**특징**:
- **복구 가능**: `Exception`은 일반적으로 프로그램이 오류를 처리하고 복구할 수 있는 경우가 많습니다.
- **예외 처리 필요**: `Exception`은 코드에서 명시적으로 처리해야 합니다. 이를 위해 `try-catch` 블록을 사용하여 예외를 처리하거나, 예외를 호출한 메서드로 전달하여 처리할 수 있습니다.
- **Checked Exception과 Unchecked Exception**:
  - **Checked Exception**: `IOException`, `SQLException`처럼 반드시 예외 처리가 요구되는 예외. 기본적으로 스프링 트랜잭션에서 롤백되지 않지만 설정을 통해 변경 가능합니다.
  - **Unchecked Exception**: `RuntimeException`을 상속받는 예외들 (예: `NullPointerException`, `ArrayIndexOutOfBoundsException`)은 선택적으로 처리할 수 있습니다. 참고로 스프링 트랜잭션에서는 반드시 롤백됩니다.

### **차이점 요약**:
- `Error`는 시스템 수준의 심각한 문제를 의미하며, 복구가 불가능하고 예외 처리가 필요하지 않습니다.
- `Exception`은 프로그램 실행 중 발생할 수 있는 문제를 의미하며, 예외 처리를 통해 복구할 수 있습니다.

따라서, **`Error`는 처리할 필요가 없으며**, **`Exception`은 적절히 처리해야** 합니다.

</details>


<details>
  <summary><h3>11. 정적 클래스와 정적 변수, 파이널에 대해 설명하세요.</h3></summary> 

### 1. **정적 클래스 (Static Class)**

- **정적 클래스**는 클래스 내부에 정의된 클래스 중 `static` 키워드가 붙은 클래스입니다. **내부 클래스**나 **중첩 클래스**에서만 정의할 수 있습니다.
- 정적 클래스는 외부 클래스의 인스턴스와는 관계없이 독립적으로 존재할 수 있습니다. 즉, **정적 클래스는 외부 클래스의 인스턴스 없이 사용할 수 있습니다**.

#### 특징:
- 외부 클래스의 인스턴스 없이 사용할 수 있습니다.
- 외부 클래스의 `static` 멤버만 접근할 수 있습니다.
- 일반적으로 **정적 클래스는 메모리 낭비를 줄이고, 효율적인 코드 작성** 에 도움이 됩니다.


### 2. **정적 변수 (Static Variable)**

- **정적 변수**는 클래스의 인스턴스와 관계없이 클래스 자체에 속하는 변수입니다. **모든 인스턴스가 동일한 메모리 공간을 공유**하므로, 클래스에 속한 **하나의 인스턴스**만 값이 변경되면 모든 인스턴스가 그 값을 공유합니다.
- **`static` 키워드를 사용**하여 클래스 레벨에서 선언된 변수입니다.

#### 특징:
- 클래스 로딩 시 한 번만 초기화되고, **모든 인스턴스가 공유**합니다.
- 객체 생성 없이 클래스 이름으로 접근할 수 있습니다.
- 주로 **상수 값** 또는 **전역적으로 공유되는 값**을 정의할 때 사용됩니다.


### 3. **파이널 (Final)**

- **`final`**은 변수, 메서드, 클래스 등에 적용할 수 있는 키워드로, 각각의 목적에 따라 다르게 동작합니다.
  
#### 1. **파이널 변수 (Final Variable)**
   - **상수**로 만들기 위해 사용됩니다. 한 번 값이 할당되면, 값을 변경할 수 없습니다.
   - **일반 변수**에 `final`을 사용하면 상수가 됩니다. 
   - 객체 참조 변수가 `final`이면 참조하는 객체의 **주소가 변경되지 않도록** 보장합니다.

#### 2. **파이널 메서드 (Final Method)**
   - 메서드에 `final`을 사용하면, **하위 클래스에서 해당 메서드를 오버라이드 할 수 없습니다**. 
   - 주로 메서드의 **동작을 변경하지 않도록** 할 때 사용됩니다.

#### 3. **파이널 클래스 (Final Class)**
   - 클래스에 `final`을 사용하면, 해당 클래스를 **상속할 수 없습니다**.
   - 주로 **상속을 막고, 클래스의 불변성을 보장**할 때 사용됩니다.


### 결론:
- **정적 클래스**: 외부 클래스의 인스턴스 없이 사용할 수 있는 클래스.
- **정적 변수**: 클래스 레벨에서 모든 인스턴스가 공유하는 변수.
- **파이널**: 값 변경 불가, 오버라이드 불가, 상속 불가 등을 보장하는 키워드.

</details>

<details>
  <summary><h3>12. 컬렉션 클래스와 스트림에 대해 설명하세요.</h3></summary> 

### 1. **컬렉션 클래스 (Collection Classes)**

컬렉션 클래스는 자바에서 데이터를 저장, 관리 및 조작하기 위한 다양한 클래스들을 제공합니다. 자바 컬렉션 프레임워크는 **데이터의 저장 방식**과 **작업에 필요한 알고리즘**을 추상화하여 제공합니다.

#### 주요 컬렉션 인터페이스:
- **List**: 순서가 있고 중복된 값을 허용하는 컬렉션. 예: `ArrayList`, `LinkedList`.
- **Set**: 순서가 없고 중복을 허용하지 않는 컬렉션. 예: `HashSet`, `TreeSet`.
- **Queue**: FIFO(선입선출) 방식의 컬렉션. 예: `LinkedList`, `PriorityQueue`.
- **Map**: 키-값 쌍으로 데이터를 저장하는 컬렉션. 예: `HashMap`, `TreeMap`.

#### 주요 컬렉션 클래스:
- **ArrayList**: 동적으로 크기가 변하는 배열 기반의 리스트. 순서가 있고 중복을 허용.
- **HashSet**: 해시 테이블 기반의 집합으로, 순서는 없고 중복을 허용하지 않음.
- **HashMap**: 키와 값의 쌍으로 데이터를 저장하며, 순서가 없고 빠른 조회 성능을 제공.
- **LinkedList**: 노드 기반의 리스트로, 양방향 연결 리스트를 사용하며 삽입과 삭제가 빠름.


### 2. **스트림 (Stream)**

자바 8에서 도입된 **스트림(Stream)**은 컬렉션의 데이터를 함수형 방식으로 처리할 수 있게 해주는 API입니다. **스트림**은 데이터의 순차적 또는 병렬적 처리 방식을 지원하며, 컬렉션을 다루는 과정에서 더욱 직관적이고 선언적인 코드 작성이 가능하게 합니다.

#### 주요 특징:
- **불변성 (Immutability)**: 스트림은 데이터를 변경하지 않고, 원본 데이터를 수정하지 않습니다.
- **지연 실행 (Lazy Evaluation)**: 스트림의 연산은 필요할 때만 실행됩니다.
- **함수형 프로그래밍**: **map()**, **filter()**, **reduce()** 등의 함수형 연산을 지원합니다.
- **병렬 처리**: 스트림은 `parallel()` 메서드를 사용하여 데이터의 병렬 처리도 지원합니다.

#### 스트림 연산:
1. **중간 연산 (Intermediate Operations)**: `map()`, `filter()`, `distinct()` 등. 중간 연산은 새로운 스트림을 반환하고, 실제 연산은 터미널 연산이 실행될 때 일어납니다.
2. **터미널 연산 (Terminal Operations)**: `collect()`, `forEach()`, `reduce()` 등. 스트림 처리의 마지막 단계로, 이 연산이 실행되면 스트림이 소비됩니다.

#### 예시:
```java
import java.util.*;
import java.util.stream.*;

public class StreamExample {
    public static void main(String[] args) {
        List<String> list = Arrays.asList("apple", "banana", "orange", "apple", "grape");

        // 스트림을 이용한 데이터 처리
        list.stream()
            .filter(fruit -> fruit.startsWith("a"))   // "a"로 시작하는 요소 필터링
            .map(String::toUpperCase)                 // 대문자로 변환
            .distinct()                               // 중복 제거
            .forEach(System.out::println);            // 출력
    }
}
```

### 결론:
- **컬렉션 클래스**는 데이터를 저장하고 관리하는 다양한 구조를 제공하며, **List**, **Set**, **Map** 등 다양한 컬렉션을 사용하여 데이터를 효율적으로 처리할 수 있습니다.
- **스트림**은 데이터를 선언적이고 함수형으로 처리할 수 있게 해주는 API로, **중간 연산**과 **터미널 연산**을 통해 데이터를 쉽게 변형하고 처리할 수 있습니다. 또한 병렬 처리 기능을 제공하여 대규모 데이터를 효율적으로 처리할 수 있습니다.

</details>

<details>
  <summary><h3>13. equals()와 hashCode() 메서드</h3></summary>

- **`equals()`**: 객체의 동등성을 비교하는 메서드로, 두 객체가 같은지 판단합니다. 일반적으로 객체의 필드 값을 기준으로 비교하며, `equals()`를 오버라이드할 경우 `hashCode()`도 함께 오버라이드해야 합니다.
  
- **`hashCode()`**: 객체의 해시 값을 반환하는 메서드로, 해시 기반 컬렉션에서 빠른 검색을 지원합니다. `equals()`가 `true`인 객체는 `hashCode()`가 같아야 하며, 반대는 아닙니다.

- **관계**: `equals()`와 `hashCode()`는 함께 사용되어야 하며, `equals()`가 `true`인 객체는 동일한 `hashCode()`를 반환해야 합니다.

#### 예시

```java
@Override
public boolean equals(Object obj) {
    if (this == obj) return true;
    if (obj == null || getClass() != obj.getClass()) return false;
    MyClass other = (MyClass) obj;
    return id == other.id;
}

@Override
public int hashCode() {
    return Objects.hash(id);
}
```

`equals()`와 `hashCode()`는 **해시 기반 컬렉션**에서 객체를 효율적으로 관리하기 위해 중요합니다.

</details>


<details>
  <summary><h3>14. 객체지향이란?</h3></summary>

**객체지향(Object-Oriented Programming, OOP)**은 소프트웨어를 객체(Object)들의 상호작용으로 구성하는 프로그래밍 패러다임입니다. 객체는 데이터와 이를 처리하는 메서드를 하나의 단위로 묶은 개념입니다.

#### 주요 개념
- **클래스(Class)**: 객체를 생성하기 위한 템플릿.
- **객체(Object)**: 클래스의 인스턴스로, 데이터를 담고 있는 실제 존재.
- **캡슐화(Encapsulation)**: 객체의 데이터를 외부에서 직접 접근하지 못하도록 보호하고, 이를 메서드를 통해 접근하도록 제한하는 것.
- **상속(Inheritance)**: 기존 클래스를 기반으로 새로운 클래스를 만드는 것.
- **다형성(Polymorphism)**: 동일한 메서드 호출이 객체의 타입에 따라 다르게 동작하는 특성.
- **추상화(Abstraction)**: 객체의 복잡성을 숨기고 필요한 부분만 공개하여 단순화하는 것.

#### 객체지향의 장점
- **재사용성**: 클래스와 객체를 재사용 가능.
- **유지보수성**: 캡슐화와 추상화 덕분에 코드 수정 시 다른 부분에 영향을 적게 미침.
- **확장성**: 상속을 통해 새로운 기능을 추가하거나 수정할 수 있음.

</details>

<details>
  <summary><h3>15. SOLID 원칙이란?</h3></summary>

**SOLID**는 객체지향 설계를 위한 5가지 기본 원칙의 약자입니다. 이 원칙들을 따르면 더 유연하고, 확장 가능하며, 유지보수가 용이한 코드를 작성할 수 있습니다.

#### 1. **단일 책임 원칙 (Single Responsibility Principle, SRP)**

- **설명**: 클래스는 하나의 책임만 가져야 한다는 원칙입니다.
- **이유**: 클래스가 여러 책임을 가지면 변경이 필요할 때 그 클래스를 수정해야 하므로 유지보수가 어렵고, 변경 사항이 의도하지 않은 문제를 일으킬 수 있습니다.

#### 2. **개방-폐쇄 원칙 (Open/Closed Principle, OCP)**

- **설명**: 소프트웨어 엔티티는 확장에는 열려 있고, 수정에는 닫혀 있어야 한다는 원칙입니다.
- **이유**: 기존 코드를 수정하지 않고 새로운 기능을 추가할 수 있도록 해야 코드의 안정성을 유지할 수 있습니다.

#### 3. **리스코프 치환 원칙 (Liskov Substitution Principle, LSP)**

- **설명**: 자식 클래스는 부모 클래스를 대체할 수 있어야 한다는 원칙입니다.
- **이유**: 상속받은 클래스는 부모 클래스의 기능을 확장하거나 수정해야 하며, 부모 클래스 객체를 자식 클래스 객체로 대체할 수 있어야 합니다.

#### 4. **인터페이스 분리 원칙 (Interface Segregation Principle, ISP)**

- **설명**: 특정 클라이언트를 위한 인터페이스는 그 클라이언트에 맞게 분리되어야 한다는 원칙입니다.
- **이유**: 인터페이스는 사용하는 쪽에 맞게 최소화해야 하며, 사용하지 않는 기능까지 강제하지 않도록 해야 합니다.

#### 5. **의존 역전 원칙 (Dependency Inversion Principle, DIP)**

- **설명**: 고수준 모듈은 저수준 모듈에 의존해서는 안 되고, 두 모듈 모두 추상화된 것에 의존해야 한다는 원칙입니다.
- **이유**: 구현이 아닌 인터페이스에 의존함으로써, 코드의 결합도를 낮추고 유연성을 높일 수 있습니다.

#### SOLID 원칙을 지키면?
- 코드의 재사용성과 확장성을 높이며, 유지보수가 용이해집니다.
- 테스트가 용이하고, 코드의 결합도를 낮출 수 있습니다.
</details>


<details>
  <summary><h3>16. 제네릭 (Generics)</h3></summary>

- **제네릭**은 클래스, 인터페이스, 메서드에서 타입을 **매개변수화**하여, 코드 재사용성과 타입 안전성을 높이는 기능입니다. 
- 타입을 **런타임이 아닌 컴파일 타임에** 결정할 수 있어, 형변환을 방지하고, 코드의 안전성을 높입니다.

#### 주요 특징
1. **타입 매개변수화**: `<>`를 사용하여 클래스나 메서드에서 타입을 변수처럼 다룰 수 있습니다.
2. **타입 안전성**: 컴파일 시 타입 체크가 이루어져, 런타임에서 발생할 수 있는 `ClassCastException`을 방지할 수 있습니다.
3. **유연성**: 같은 로직을 다양한 타입에 대해 사용할 수 있습니다.

#### 예시

```java
// 제네릭을 사용하는 클래스
public class Box<T> {
    private T value;

    public T getValue() {
        return value;
    }

    public void setValue(T value) {
        this.value = value;
    }
}

// 사용 예
Box<Integer> intBox = new Box<>();
intBox.setValue(10);
System.out.println(intBox.getValue());  // 10

Box<String> strBox = new Box<>();
strBox.setValue("Hello");
System.out.println(strBox.getValue());  // Hello
```

#### 제네릭의 장점
1. **형변환을 줄여줌**: 코드에서 객체의 타입을 명시적으로 지정하여 안전하게 사용할 수 있습니다.
2. **코드 재사용**: 동일한 로직을 다양한 타입에 대해 사용할 수 있습니다.

</details>
