- **Spring DI/IoC는 어떻게 동작하나요?**
    
    Spring의 IoC, 즉 제어의 역전은 객체의 생성과 생명주기 관리를 개발자가 아닌 Spring 컨테이너가 맡는 개념입니다. 전통적으로는 객체가 직접 의존 객체를 생성해서 강하게 결합되지만, IoC를 통해 이런 제어 권한을 Spring에 넘겨서 결합도를 낮춥니다.
    
    DI(Dependency Injection)는 IoC를 구현하는 방식 중 하나로, 필요한 의존 객체를 외부에서 주입받는 방법입니다. 예를 들어 생성자 주입, 필드 주입(`@Autowired`) 등이 있습니다.
    
    이렇게 하면 객체 간 결합도가 낮아져 유지보수와 확장성이 좋아지고, 테스트할 때도 Mock 객체 주입이 쉬워집니다."
    
- **Spring 빈의 생성 과정과 생명주기**
    
    Spring 빈은 Spring 컨테이너가 생성부터 소멸까지 전 과정을 관리합니다. 먼저, `ApplicationContext`가 초기화되면서 설정 정보를 바탕으로 빈들을 생성합니다.
    
    빈 생성 후에는 `@Autowired`나 생성자 주입으로 의존성을 주입받고, `@PostConstruct` 또는 `InitializingBean`의 `afterPropertiesSet()` 메서드로 초기화 작업을 수행합니다.
    
    이후 빈이 사용되고, 애플리케이션 종료 시에는 `@PreDestroy` 또는 `DisposableBean`의 `destroy()`를 통해 소멸 전 필요한 정리 작업을 합니다.
    
    또한, 빈은 기본적으로 싱글톤으로 관리되지만, `prototype`, `request`, `session` 등 다양한 스코프도 지원합니다.
    
    이 생명주기 과정을 이해하면 초기화와 종료 시 필요한 작업을 안전하게 처리해 애플리케이션 안정성 및 확장성을 높일 수 있습니다
    
- **Spring Web MVC의 DispatcherServlet 동작 원리**
    
    DispatcherServlet은 Spring MVC의 중앙 컨트롤러(Front Controller) 역할을 하는 서블릿으로, 클라이언트의 모든 HTTP 요청을 처음 받아 처리합니다.
    
    요청이 들어오면 DispatcherServlet은 먼저 HandlerMapping을 통해 요청 URL에 맞는 적절한 컨트롤러를 찾습니다.
    그 다음, HandlerAdapter를 통해 해당 컨트롤러의 메서드를 실행하여 비즈니스 로직을 처리합니다.
    컨트롤러는 처리 결과와 뷰 이름을 담은 ModelAndView 객체를 반환하고, DispatcherServlet은 ViewResolver를 사용해 뷰를 결정합니다.
    마지막으로, 선택된 뷰가 렌더링되어 HTML 등의 응답이 클라이언트에 전송됩니다.
    
    이 과정에서 DispatcherServlet은 요청과 응답 흐름을 중앙에서 관리하며, HandlerMapping, HandlerAdapter, ViewResolver 같은 주요 컴포넌트가 역할을 분담하여 협력합니다.
    즉, DispatcherServlet은 Spring MVC 요청 처리의 핵심 허브라고 할 수 있습니다.
    
- **Servlet Filter와 Spring Interceptor의 차이**
    
    Servlet Filter와 Spring Interceptor는 둘 다 요청을 가로채서 처리하는 역할을 하지만, 동작하는 위치와 역할에 차이가 있습니다.
    
    먼저, Servlet Filter는 서블릿 컨테이너 단계에서 동작해서 모든 요청과 응답을 처리할 수 있습니다. 그래서 인코딩 처리, 보안, CORS, 정적 리소스 처리 같은 애플리케이션 전반에 영향을 주는 작업에 주로 사용됩니다. Spring에 종속적이지 않고, `@WebFilter`나 `web.xml`에서 설정합니다.
    
    반면에 Spring Interceptor는 Spring MVC의 DispatcherServlet 이후에 동작해서, 컨트롤러가 실행되기 전과 후에 추가 작업을 할 수 있습니다. 그래서 로그인 체크, 권한 검증, 로깅 등 비즈니스 로직과 관련된 요청 전후 처리를 할 때 주로 활용합니다. `HandlerInterceptor`를 구현하고 `WebMvcConfigurer`에 등록하는 방식으로 사용합니다.
    
- **스프링(Spring)과 스프링 부트(Spring Boot)의 차이**
    - **Spring**: Java 기반의 웹 프레임워크로, DI, AOP 등 다양한 기능 제공하지만 설정이 복잡함
    - **Spring Boot**: Spring을 편리하게 사용할 수 있도록 만든 프레임워크로, **자동 설정**, **내장 웹 서버**, **단순한 배포** 지원
- **AOP와 @Aspect의 동작 원리**
    
    AOP, 즉 Aspect-Oriented Programming은 핵심 비즈니스 로직과 공통 관심사(예: 로깅, 트랜잭션, 보안 등)를 분리해서 중복 코드를 줄이고 유지보수를 쉽게 하는 프로그래밍 기법입니다.
    
    Spring에서 AOP는 주로 프록시 기반으로 동작하는데, 대상 객체를 프록시가 감싸서 메서드 실행 전후에 공통 로직을 적용합니다. 이 때 `@Aspect` 어노테이션을 붙인 클래스를 스프링이 인식해서 자동으로 프록시를 생성합니다.
    
    예를 들어, `@Before` 어노테이션은 지정한 메서드가 실행되기 전에 공통 작업을 수행하도록 하고, `@After`, `@Around` 등 다양한 어노테이션을 통해 메서드 실행 전, 후, 예외 발생 시 등 원하는 시점에 코드를 실행할 수 있습니다.
    
    이런 구조 덕분에 핵심 로직은 깔끔하게 유지하면서, 공통 기능을 모듈화하여 재사용성과 유지보수성을 크게 높일 수 있습니다.
    
- **@Transactional 은 어떤 기능을 하나요?**
    - "`@Transactional`은 트랜잭션을 관리하는 어노테이션으로, 메서드 실행 시 트랜잭션을 시작하고 정상 종료 시 자동으로 커밋, 예외 발생 시 롤백하는 기능을 제공합니다."
    - `@Transactional(readOnly = true)`는 변경 감지를 비활성화하여 성능을 최적화하지만, 영속성 컨텍스트는 유지되므로 Lazy Loading 같은 기능은 정상 작동합니다.
- **Tomcat이 정확히 어떤 역할을 하는 도구인가요?**
    
    "Tomcat은 Java 기반 웹 애플리케이션을 실행하는 WAS(Web Application Server)입니다.”
    
    ✔ **주요 기능**
    
    - **Servlet 컨테이너 역할**: 서블릿을 실행하고, HTTP 요청/응답을 처리
    - **JSP 실행**: JSP(Java Server Pages) 파일을 컴파일하여 동적으로 HTML 생성
    - **세션 관리**: HTTP 세션을 유지 및 관리
    - **멀티스레드 처리**: 요청마다 새로운 스레드를 생성하여 병렬 처리
- **STOMP와 WebSocket에 대해 말해주세요**
    
    > WebSocket
    > 
    
    TCP 위에서 동작하는 양방향 프로토콜 
    
    > STOMP
    > 
    
    WebSocket 위에서 동작하는 서브프로토콜, 프레임 구조 명확하고 구현된 명령어를 통해서 채널기반 pub-sub 모델 구현이 가능하다. 또한 메시지 브로커와 연동도 용이한편
    
    즉, STOMP는 WebSocket을 더 구조적으로 쓰게 해주는 기술이다.
    
    > STOMP 커넥션 관리 및 스레드 할당
    > 
    
    Spring에서 STOMP 기반 WebSocket 사용 시, 내부적으로 다음 컴포넌트들이 존재한다.
    
    - ClientInboundChannel(클라이언트 → 서버 처리)
    - ClientOutboundChannel(서버 → 클라언트 처리)
    - BrokerChannel(브로커 내부 라우팅, 세션 방식처럼 저장)
    
    이 각각은 ExecutorSubscribableChannel로 구성돼있고, 각각 별도 스레드풀에서 비동기 처리
    
    > 메시지 처리 흐름 @MessageMapping 기준
    > 
    1. 클라이언트가 WebSocket을 통해 메시지를 전달
    2. 메시지는 ClientInboundChannel을 통해 메시지 핸들러로 라우팅
    3. 해당 핸들러가 @MessageMapping가 붙은 메서드 호출
    4. 리턴 값은 ClientOutboundChannel가 브로커로 전달
    5. 브로커는 구독 중인 대상에게 메시지 브로드케스트
- 스프링 생태계에 대해 설명해주세요
    
    스프링은 자바 플랫폼을 위한 경량 애플리케이션 프레임워크로, 핵심적으로 두 가지 중요한 개념을 기반으로 합니다.
    
    첫 번째는 **DI(Dependency Injection, 의존성 주입)**입니다. DI는 객체 간의 의존 관계를 외부에서 주입받는 방식으로, 객체 간 결합도를 낮추고 OCP(개방-폐쇄 원칙)를 지키는 데 도움을 줍니다. 이로 인해 객체의 생성과 관리 책임이 개발자가 아닌 스프링 컨테이너로 위임되며, 유연한 코드 구조를 만들 수 있습니다.
    
    두 번째는 **IoC(Inversion of Control, 제어의 역전)**입니다. 스프링에서는 IoC 컨테이너가 애플리케이션의 구성 요소들을 빈(Bean)으로 등록하고, 애플리케이션 구동 시점에 이들을 싱글톤으로 생성해 관리합니다. 이를 통해 객체 생성, 의존성 주입, 생명주기 관리 등을 자동화할 수 있습니다.
    
    스프링 생태계는 이러한 핵심 기술을 바탕으로 다양한 모듈로 확장되어 있습니다. 제가 알고 있는 주요 구성 요소는 다음과 같습니다.
    
    - **Spring Boot**: 복잡한 설정을 자동화해주며, 빠른 애플리케이션 개발을 지원합니다.
    - **Spring Data**: JPA, MongoDB 등 다양한 데이터 저장소와의 연동을 간편하게 도와주는 모듈입니다.
    - **Spring Batch**: 대용량 데이터의 일괄 처리 작업을 효율적으로 처리할 수 있게 해주는 프레임워크입니다.
    - **Spring Security**: 인증과 권한 관리를 포함한 보안 기능을 담당합니다.
    - **Spring Cloud**: 마이크로서비스 아키텍처에서 서비스 간 통신, 구성 관리, 장애 복구 등을 지원합니다.
    
    이처럼 스프링 생태계는 다양한 개발 상황에 맞춰 사용할 수 있는 강력한 도구들을 제공하며, 유연하고 확장성 있는 애플리케이션 개발을 가능하게 합니다.
    
- DI 방식에 대해
    
    DI 방식에는 생성자, 필드, 세터 주입이 있고, 일반적으로는 불변성과 테스트 용이성이 좋은 생성자 주입을 가장 권장합니다.
