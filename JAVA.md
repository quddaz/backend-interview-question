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
  <summary><h3>7. Wrapper Class가 무엇인가요?</h3></summary>
자바에는 기본 타입과 추가로 Wrapper 
</details>
