# JAVA 

- **JVM의 구조와 Java의 실행방식이 뭔가요?**
    
    JVM은 자바 프로그램을 실행하는 가상 머신으로, 운영체제에 독립적인 환경을 제공합니다. JVM은 클래스 로더, 메모리 영역, 실행 엔진으로 구성되어 있는데요, 클래스 로더가 바이트코드를 읽어오고, 메모리 영역에는 클래스 정보, 객체, 변수들이 저장됩니다. 실행 엔진은 바이트코드를 해석하거나 JIT 컴파일을 통해 기계어로 변환해 실행합니다. 이렇게 자바는 소스코드를 컴파일해 바이트코드로 만들고, JVM이 이를 실행하는 방식으로 동작합니다.
    
- **Call by value와 Call by Reference에 대해 설명해주세요.**
    
    Call by Value와 Call by Reference는 함수나 메서드에 인자를 전달하는 방식입니다.
    Call by Value는 값 자체를 복사해서 넘기는 방식으로, 함수 내부에서 값을 변경해도 원본에는 영향이 없습니다.
    반면 Call by Reference는 변수의 주소를 넘겨서 함수 내부에서 값을 바꾸면 원본도 같이 변경됩니다.
    
    자바는 기본 자료형은 Call by Value 방식으로 값을 복사해서 넘기고, 객체는 참조 값(주소)을 복사해서 넘깁니다.
    
- **Primitive type & Reference type에 대해 설명해주세요**
    
    자바의 타입은 크게 기본형(Primitive type)과 참조형(Reference type)으로 나눌 수 있습니다.
    
    기본형은 int, boolean, double 등 총 8가지가 있고, 값 자체가 스택 메모리에 저장됩니다. 이들은 객체가 아니기 때문에 null 값을 가질 수 없습니다.
    
    반면 참조형은 클래스, 배열, 인터페이스, 열거형 등이 포함되며, 변수에는 객체가 저장된 힙 메모리 주소인 참조값이 저장됩니다. 참조형은 null 값을 가질 수 있고, String 같은 경우는 불변 객체로 특별히 관리됩니다.
    
- **Wrapper Class가 무엇인가요?**
    
    Wrapper 클래스는 자바의 기본 타입(Primitive type)을 객체로 다룰 수 있도록 감싸주는 클래스입니다. 예를 들어, int의 Wrapper 클래스는 Integer입니다.
    
    이 클래스들을 사용하는 주된 이유는 자바 컬렉션 같은 객체만 저장할 수 있는 구조에서 기본 타입을 사용하기 위해서입니다.
    
    또한, Wrapper 클래스는 다양한 유틸리티 메서드를 제공하며, 자바는 자동으로 기본 타입과 Wrapper 클래스 간 변환을 해주는 오토박싱과 언박싱 기능도 지원합니다.
    
    다만, Wrapper 클래스는 기본 타입보다 메모리를 더 사용하기 때문에 꼭 필요한 경우에만 사용하는 게 좋습니다.”
    
- **직렬화는 무엇이고 java에서는 왜 사용하나요?**
    
    직렬화는 객체를 바이트 스트림 형태로 변환하여 저장하거나 전송하는 기술입니다. 이 기술은 객체 자체를 메모리 주소로 전달하므로 Reference Type의 타입의 데이터들은 다른 OS나 환경에서는 전달이 불가능합니다. 그렇기에 만들어진 기술입니다.
    
- **String 클래스와 StringBuffer, StringBuilder 특징**
    
    String 클래스는 불변(Immutable) 객체입니다. 즉, 문자열이 한 번 생성되면 변경할 수 없으며, 변경 시 새로운 String 객체가 생성됩니다. 이는 보안성을 높이고, 해시값을 캐싱하여 성능을 최적화하는 등의 장점이 있습니다. 하지만 문자열을 자주 변경하면 메모리 낭비가 발생할 수 있습니다.
    
    이를 해결하기 위해 **가변(Mutable) 문자열 객체인 StringBuffer와 StringBuilder**가 제공됩니다.
    
    - StringBuffer: 멀티스레드 환경에서 안전(Thread-Safe)하며, synchronized 키워드로 동기화가 적용되어 있습니다.
    - StringBuilder: 싱글스레드 환경에서 빠른 성능을 제공합니다. 동기화가 없으므로 멀티스레드 환경에서는 안전하지 않습니다.
- **Casting(업캐스팅 & 다운캐스팅)의 필요성에 대해 설명하세요.**
    
    캐스팅은 객체 타입 변환을 의미하며, 크게 업캐스팅과 다운캐스팅으로 나뉩니다.
    
    업캐스팅은 자식 클래스 타입을 부모 클래스 타입으로 자동 변환하는 것으로, 다형성을 활용할 때 주로 사용합니다. 예를 들어, 자식 객체를 부모 타입으로 참조하면 코드가 유연해지고 공통 메서드를 호출할 수 있습니다.
    
    반면, 다운캐스팅은 부모 클래스 타입을 자식 클래스 타입으로 명시적으로 변환하는 것이고, 자식 클래스에만 있는 특화된 기능을 사용하기 위해 필요합니다. 이때는 반드시 실제 객체 타입인지 확인해야 하며, 그렇지 않으면 ClassCastException이 발생할 수 있습니다.
    
    스프링 같은 프레임워크에서는 서비스 인터페이스와 구현체 관계에서 주로 업캐스팅을 사용해 코드의 확장성과 유지보수성을 높입니다
    
- **Thread에 대해 설명하세요.**
    
    스레드는 프로세스 내에서 실행되는 가벼운 실행 단위입니다. 하나의 프로세스는 여러 스레드를 가질 수 있고, 이 스레드들은 메모리와 자원을 공유하기 때문에 스레드 간 통신이 빠릅니다. 멀티스레딩을 통해 동시에 여러 작업을 처리할 수 있어 프로그램의 처리 효율을 높일 수 있습니다.
    
    결론적으로 스레드는 멀티태스킹과 병렬처리를 구현하는 기본 단위입니다.
    
- **Garbage Collection에 대해 설명하세요.**
    
    Garbage Collection, 즉 GC는 자바에서 사용하지 않는 객체를 자동으로 메모리에서 해제하는 기능입니다. 개발자가 직접 메모리를 관리하지 않아도 되어 메모리 누수를 방지하고 효율적인 메모리 사용을 돕습니다.
    
    GC는 힙 영역에서 동작하며, 참조되지 않는 객체를 찾아 제거합니다. 주요 과정은 살아있는 객체를 표시(mark)하고, 필요 없는 객체를 정리(sweep)하며, 메모리 단편화를 줄이기 위해 압축(compact)하기도 합니다.
    
- **Error와 Exception**
    
    Error와 Exception은 자바에서 예외 처리 시 구분하는 두 가지 개념입니다.
    Error는 시스템 수준에서 발생하는 치명적인 문제로, 예를 들어 메모리 부족이나 스택 오버플로우 같은 상황입니다. 이런 오류는 보통 복구가 불가능하며, 개발자가 직접 처리하지 않아도 됩니다.
    
    반면 Exception은 프로그램 실행 중 발생하는 예외 상황으로, NullPointerException, IOException 등이 있습니다. Exception은 적절히 처리하여 프로그램이 정상적으로 동작하도록 복구할 수 있습니다.
    Exception에는 반드시 처리해야 하는 Checked Exception과 선택적으로 처리 가능한 Unchecked Exception이 있습니다.
    
    정리하면, Error는 시스템 오류라서 보통 처리하지 않고, Exception은 코드에서 예외 처리를 통해 대응해야 하는 상황입니다
    
- **정적 클래스(static class)와 정적 변수, 파이널(final)에 대해 설명하세요.**
    
    정적 클래스는 클래스 내부에 선언된 `static` 중첩 클래스로, 외부 클래스의 인스턴스 없이 사용할 수 있습니다. 정적 클래스는 외부 클래스의 `static` 멤버만 접근할 수 있죠.
    
    정적 변수는 `static` 키워드가 붙은 변수로, 모든 인스턴스가 하나의 메모리를 공유합니다. 따라서 클래스 이름으로 직접 접근할 수 있고, 주로 공통된 값을 저장할 때 사용됩니다.
    
    마지막으로 `final` 키워드는 변수, 메서드, 클래스에 적용되는데요,
    
    - 변수에 붙으면 한 번 초기화 후 값 변경이 불가능한 상수가 되고,
    - 메서드에 붙으면 하위 클래스에서 오버라이드할 수 없으며,
    - 클래스에 붙으면 상속을 막아 변경을 제한합니다.
    
    이렇게 `static`과 `final`은 각각 메모리 관리와 불변성, 상속 통제에 중요한 역할을 합니다.
    
- **Collection Class와 Stream에 대해 설명하세요.**
    
    컬렉션 클래스는 자바에서 데이터를 저장하고 관리하는 다양한 자료구조를 제공합니다. 대표적으로 List, Set, Map 등이 있습니다.
    
    스트림은 자바 8에서 도입된 API로, 컬렉션의 데이터를 함수형 프로그래밍 방식으로 처리할 수 있게 해줍니다. 스트림은 데이터를 직접 변경하지 않고, 중간 연산과 터미널 연산을 통해 필터링, 매핑, 집계 등의 처리를 선언적으로 할 수 있습니다. 또한 병렬 처리도 지원해 대용량 데이터 처리에 효율적입니다.
    
    요약하면, 컬렉션은 데이터를 저장하는 구조이고, 스트림은 그 데이터를 처리하는 강력한 도구라고 볼 수 있습니다.
    
- **equals()와 hashCode() 메서드**
    
    `equals()` 메서드는 두 객체가 논리적으로 같은지를 비교합니다. 보통 객체의 중요한 필드 값을 기준으로 비교하며, 오버라이드할 때는 `hashCode()`도 반드시 함께 오버라이드해야 합니다.
    
    `hashCode()`는 객체의 해시 값을 반환하는 메서드로, 해시 기반 컬렉션(HashMap, HashSet 등)에서 빠른 검색과 저장을 가능하게 합니다. 중요한 규칙은, `equals()`가 true를 반환하는 두 객체는 반드시 같은 `hashCode()` 값을 가져야 한다는 것입니다.
    
    따라서 `equals()`와 `hashCode()`는 항상 같이 재정의하여 객체의 동등성과 해시값 일관성을 보장해야 해, 컬렉션에서 제대로 작동할 수 있습니다.
    
- **객체지향(OOP)이란?**
    
    객체지향 프로그래밍, 즉 OOP는 소프트웨어를 객체들의 상호작용으로 구성하는 프로그래밍 방법입니다. 객체는 데이터와 그 데이터를 처리하는 메서드를 하나로 묶은 단위입니다.
    
    주요 개념으로는
    
    - 클래스는 객체를 만들기 위한 설계도이고,
    - 객체는 클래스의 실제 인스턴스입니다.
    - 캡슐화는 데이터 접근을 제한해 보호하는 것이고,
    - 상속은 기존 클래스를 확장하는 것이며,
    - 다형성은 같은 메서드 호출이 객체에 따라 다르게 동작하는 특성입니다.
    - 추상화는 복잡한 내용을 숨기고 필요한 부분만 보여주는 것입니다.
    
    객체지향은 재사용성, 유지보수성, 확장성이 뛰어나 개발 효율성과 코드 품질을 높여줍니다.
    
- **SOLID 원칙이란?**
    
    **SOLID**는 객체지향 설계를 위한 5가지 기본 원칙의 약자입니다. 이 원칙들을 따르면 더 유연하고, 확장 가능하며, 유지보수가 용이한 코드를 작성할 수 있습니다.
    
    **1. 단일 책임 원칙 (Single Responsibility Principle, SRP)**
    
    - **설명**: 클래스는 하나의 책임만 가져야 한다는 원칙입니다.
    - **이유**: 클래스가 여러 책임을 가지면 변경이 필요할 때 그 클래스를 수정해야 하므로 유지보수가 어렵고, 변경 사항이 의도하지 않은 문제를 일으킬 수 있습니다.
    
    **2. 개방-폐쇄 원칙 (Open/Closed Principle, OCP)**
    
    - **설명**: 소프트웨어 엔티티는 확장에는 열려 있고, 수정에는 닫혀 있어야 한다는 원칙입니다.
    - **이유**: 기존 코드를 수정하지 않고 새로운 기능을 추가할 수 있도록 해야 코드의 안정성을 유지할 수 있습니다.
    
    **3. 리스코프 치환 원칙 (Liskov Substitution Principle, LSP)**
    
    - **설명**: 자식 클래스는 부모 클래스를 대체할 수 있어야 한다는 원칙입니다.
    - **이유**: 상속받은 클래스는 부모 클래스의 기능을 확장하거나 수정해야 하며, 부모 클래스 객체를 자식 클래스 객체로 대체할 수 있어야 합니다.
    
    **4. 인터페이스 분리 원칙 (Interface Segregation Principle, ISP)**
    
    - **설명**: 특정 클라이언트를 위한 인터페이스는 그 클라이언트에 맞게 분리되어야 한다는 원칙입니다.
    - **이유**: 인터페이스는 사용하는 쪽에 맞게 최소화해야 하며, 사용하지 않는 기능까지 강제하지 않도록 해야 합니다.
    
    **5. 의존 역전 원칙 (Dependency Inversion Principle, DIP)**
    
    - **설명**: 고수준 모듈은 저수준 모듈에 의존해서는 안 되고, 두 모듈 모두 추상화된 것에 의존해야 한다는 원칙입니다.
    - **이유**: 구현이 아닌 인터페이스에 의존함으로써, 코드의 결합도를 낮추고 유연성을 높일 수 있습니다.
    
    **SOLID 원칙을 지키면?**
    
    - 코드의 재사용성과 확장성을 높이며, 유지보수가 용이해집니다.
    - 테스트가 용이하고, 코드의 결합도를 낮출 수 있습니다.
- **제네릭 (Generics)에 대해 설명하세요.**
    - **제네릭**은 클래스, 인터페이스, 메서드에서 타입을 **매개변수화**하여, 코드 재사용성과 타입 안전성을 높이는 기능입니다.
    - 타입을 **런타임이 아닌 컴파일 타임에** 결정할 수 있어, 형변환을 방지하고, 코드의 안전성을 높입니다.
    
    **주요 특징**
    
    1. **타입 매개변수화**: `<>`를 사용하여 클래스나 메서드에서 타입을 변수처럼 다룰 수 있습니다.
    2. **타입 안전성**: 컴파일 시 타입 체크가 이루어져, 런타임에서 발생할 수 있는 `ClassCastException`을 방지할 수 있습니다.
    3. **유연성**: 같은 로직을 다양한 타입에 대해 사용할 수 있습니다.
    
    **예시**
    
    ```
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
    
    **제네릭의 장점**
    
    1. **형변환을 줄여줌**: 코드에서 객체의 타입을 명시적으로 지정하여 안전하게 사용할 수 있습니다.
    2. **코드 재사용**: 동일한 로직을 다양한 타입에 대해 사용할 수 있습니다.
- **Java 에서 Annotation 은 어떤 기능을 하나요?**
    
    "Java에서 Annotation은 메타데이터를 제공하여 코드에 대한 추가 정보를 컴파일러나 런타임 환경에서 활용할 수 있도록 합니다. 주로 컴파일 시 체크, 리플렉션(Reflection)을 활용한 동적 처리, 코드 자동 생성 등에 사용됩니다.
