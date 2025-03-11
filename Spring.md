# Spring

<details>
  <summary><h3>1. Spring DI/IoC는 어떻게 동작하나요?</h3></summary>
  
  Spring의 DI(Dependency Injection)와 IoC(Inversion of Control)는 객체의 생성과 의존성 관리를 프레임워크가 담당하도록 하여, 결합도를 낮추고 유지보수성을 높이는 개념입니다.  

  ### 1. IoC(제어의 역전)의 등장 배경
  - 전통적인 객체 지향 프로그래밍(OOP)에서는 클래스 간의 의존성이 높아질수록 코드가 복잡해지고 변경이 어려워지는 문제가 발생합니다.
  - 예를 들어, `A` 객체가 `B` 객체를 필요로 한다면, `A`가 직접 `B`를 생성(`new B()`)하게 됩니다. 하지만 이렇게 하면 `A`와 `B`가 강하게 결합되어 확장성과 테스트가 어려워집니다.
  - IoC는 이러한 문제를 해결하기 위해 **"객체의 생성 및 라이프사이클 관리를 개발자가 아닌 컨테이너(Spring)가 담당"** 하도록 하는 개념입니다.  

  ### 2. DI(의존성 주입)의 등장 배경
  - IoC를 적용하면 객체의 생성과 관리를 프레임워크가 담당하게 되는데, 이렇게 생성된 객체들을 서로 연결하는 방식이 필요합니다.
  - DI는 필요한 객체를 직접 생성하는 것이 아니라, **외부에서 주입받도록 설계하여 유연성을 높이는 방식** 입니다.
  - 예를 들어, 생성자 주입, 필드 주입(`@Autowired`), 메서드 주입을 활용하여 객체 간의 관계를 정의할 수 있습니다.

  ### 3. IoC와 DI의 관계
  - **IoC**는 큰 개념으로, 제어의 흐름을 개발자가 아닌 컨테이너(Spring)가 담당하는 것을 의미합니다.
  - **DI**는 IoC를 구현하는 방법 중 하나로, 객체의 의존성을 외부에서 주입하는 방식입니다.

  ### 4. Spring에서 IoC/DI 적용 방식
  - `@ComponentScan`을 통해 특정 패키지를 스캔하여 자동으로 Bean을 등록합니다.
  - `@Bean`을 사용하여 수동으로 Bean을 등록할 수도 있습니다.
  - `@Autowired`, `@Inject`, 생성자 주입 등을 활용하여 객체의 의존성을 주입받을 수 있습니다.

  **결론적으로**, IoC와 DI를 활용하면 객체 간의 결합도를 낮추고, 유지보수성과 확장성을 높일 수 있으며, 테스트도 용이해집니다.

</details>

<details>
  <summary><h3>2. Spring 빈의 생성 과정과 생명주기</h3></summary>
  
  Spring에서는 객체(Bean)의 생성부터 소멸까지의 전 과정을 **Spring 컨테이너**가 관리합니다. 이를 **Spring 빈의 생명주기**라고 하며, 주요 과정은 다음과 같습니다.  

  ---

  ## 1. 스프링 빈의 생성 과정

  1. **스프링 컨테이너 초기화**
     - `ApplicationContext` 또는 `BeanFactory`가 초기화됩니다.
     - 설정 정보(`@Configuration`, `@ComponentScan`, `@Bean` 등)를 기반으로 Bean 목록을 생성합니다.

  2. **Bean 생성**
     - `@Component`, `@Service`, `@Repository`, `@Configuration` 등을 사용한 클래스들이 빈으로 등록됩니다.
     - 수동 등록된 `@Bean` 메서드도 빈으로 생성됩니다.

  3. **의존성 주입(DI)**
     - `@Autowired`, 생성자 주입, 필드 주입 등을 통해 빈 간의 의존성이 주입됩니다.

  4. **초기화 콜백(InitializingBean, @PostConstruct)**
     - `@PostConstruct` 또는 `InitializingBean` 인터페이스의 `afterPropertiesSet()`이 실행됩니다.
     - 개발자가 초기화 로직을 정의할 수 있습니다.

  5. **빈 사용**
     - 클라이언트 코드에서 빈을 사용합니다.

  6. **소멸 전 콜백(DisposableBean, @PreDestroy)**
     - 애플리케이션 종료 시, `@PreDestroy` 또는 `DisposableBean` 인터페이스의 `destroy()` 메서드가 호출됩니다.

  7. **빈 소멸**
     - 스프링 컨테이너가 종료되면서 빈이 소멸됩니다.

  ---

  ## 2. 스프링 빈의 생명주기 단계

  | 단계 | 설명 |
  |------|------|
  | **1. 객체 생성** | `new`를 통해 객체가 생성됨 |
  | **2. 의존성 주입** | `@Autowired`, 생성자 주입 등을 통해 필요한 빈을 주입 |
  | **3. 초기화(InitializingBean, @PostConstruct)** | 빈 사용 전에 초기화 로직 실행 |
  | **4. 사용** | 클라이언트가 빈을 사용 |
  | **5. 소멸(DisposableBean, @PreDestroy)** | 빈이 제거되기 전에 정리 작업 실행 |
 ## 3. 스프링 빈 스코프

  스프링 빈은 스코프(Scope)에 따라 생성 및 관리 방식이 달라집니다.  

  | 스코프 | 설명 |
  |------|------|
  | **singleton** (기본값) | 애플리케이션 실행 시 한 번 생성되어 컨테이너 종료까지 유지됨 |
  | **prototype** | 요청할 때마다 새로운 인스턴스를 생성 |
  | **request** | HTTP 요청이 들어올 때마다 새로운 빈 생성 (웹 환경) |
  | **session** | HTTP 세션마다 새로운 빈 생성 (웹 환경) |
  | **application** | 서블릿 컨텍스트 별로 하나의 빈을 생성 |
  
  **결론적으로**, Spring 빈의 생명주기를 이해하면 초기화 및 소멸 과정에서 필요한 로직을 안전하게 수행할 수 있으며, 애플리케이션의 안정성을 높일 수 있습니다.

</details>

<details>
  <summary><h3>3. Spring Web MVC의 DispatcherServlet 동작 원리</h3></summary>

  ## 1. DispatcherServlet이란?
  **DispatcherServlet**은 Spring MVC에서 **중앙 컨트롤러(Front Controller)** 역할을 하는 서블릿입니다.  
  클라이언트의 모든 요청을 받아서 적절한 **컨트롤러, 서비스, 뷰**로 요청을 전달하고 응답을 반환하는 핵심 역할을 합니다.

  ---

  ## 2. DispatcherServlet의 동작 흐름

  1. **클라이언트 요청** → 브라우저에서 HTTP 요청 발생
  2. **DispatcherServlet이 요청 수신**  
     - `web.xml` 또는 `@SpringBootApplication`에서 등록된 `DispatcherServlet`이 요청을 가로챔
  3. **HandlerMapping을 통해 컨트롤러 검색**  
     - 요청 URL에 맞는 적절한 컨트롤러(핸들러)를 찾음
  4. **HandlerAdapter를 통해 컨트롤러 실행**  
     - 컨트롤러의 메서드를 실행하여 로직 처리
  5. **컨트롤러가 ModelAndView 반환**  
     - 처리 결과(모델)와 응답할 뷰 정보를 DispatcherServlet에 전달
  6. **ViewResolver를 통해 View 결정**  
     - 반환된 뷰 이름을 기반으로 적절한 뷰(JSP, Thymeleaf 등) 선택
  7. **렌더링 후 응답 반환**  
     - 최종적으로 HTML을 생성하여 클라이언트에게 반환

  ---

  ## 3. DispatcherServlet 동작 과정 예제

  **요청 예시:**  
  ```
  GET /users
  ```

  **DispatcherServlet 동작 과정**
  ```plaintext
  1. 클라이언트 → http://example.com/users 요청
  2. DispatcherServlet → HandlerMapping에서 "/users"에 해당하는 컨트롤러 검색
  3. UserController의 메서드 실행
  4. 컨트롤러가 "userList"라는 뷰 이름과 데이터를 반환
  5. ViewResolver → "userList.jsp" 뷰를 선택
  6. JSP가 렌더링되어 클라이언트에게 HTML 응답
  ```
  ---

  ## 4. DispatcherServlet의 주요 컴포넌트

  | 컴포넌트 | 역할 |
  |----------|------|
  | **HandlerMapping** | 요청을 처리할 컨트롤러를 찾음 |
  | **HandlerAdapter** | 컨트롤러를 실행하여 로직 수행 |
  | **ViewResolver** | 뷰 이름을 실제 View(JSP, Thymeleaf 등)로 변환 |
  | **ModelAndView** | 컨트롤러에서 반환하는 데이터와 뷰 정보를 담는 객체 |

  ---

  ## 5. 결론
  - DispatcherServlet은 **Spring MVC의 핵심 컨트롤러** 역할을 수행
  - **HandlerMapping → Controller → ViewResolver** 과정을 거쳐 응답 반환
  - 개발자는 **컨트롤러와 뷰만 작성하면** Spring이 나머지를 자동으로 처리

</details>

<details>
  <summary><h3>4. Servlet Filter와 Spring Interceptor의 차이</h3></summary>

  ## 1. Servlet Filter와 Spring Interceptor란?

  - **Servlet Filter**  
    - 웹 애플리케이션의 **가장 앞단**에서 요청과 응답을 가로채는 기능  
    - 요청(Request) 또는 응답(Response)을 **변경, 로깅, 인증 처리** 등에 활용  

  - **Spring Interceptor**  
    - Spring MVC의 DispatcherServlet과 Controller 사이에서 요청을 가로채는 기능  
    - **Controller 실행 전후에 추가 작업**(로그인 체크, 로깅, 데이터 검증 등)을 수행  

  ---

  ## 2. Filter와 Interceptor의 주요 차이점

  | 비교 항목 | Servlet Filter | Spring Interceptor |
  |-----------|---------------|--------------------|
  | **적용 위치** | DispatcherServlet **이전** | DispatcherServlet **이후** |
  | **처리 대상** | 모든 요청 (정적 리소스 포함) | Spring MVC의 **Handler(Controller) 요청만** |
  | **설정 방법** | `@WebFilter` 또는 `web.xml` | `HandlerInterceptor` 구현 후 `WebMvcConfigurer`에 등록 |
  | **전/후 처리** | 요청 및 응답을 모두 가로챌 수 있음 | 주로 **Controller 실행 전후** 처리 |
  | **사용 목적** | 인증, 보안, 인코딩, 로깅, 압축 | 로그인 체크, 권한 검증, 로깅, 데이터 가공 |
  | **Spring MVC 의존 여부** | ❌ (Servlet 기반, Spring과 무관) | ✅ (Spring MVC의 기능) |

  ---

  ## 3. Servlet Filter 예제

  ```java
  @WebFilter("/*") // 모든 요청에 대해 필터 적용
  public class CustomFilter implements Filter {
      @Override
      public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
              throws IOException, ServletException {
          System.out.println("요청 도착 - Filter 실행");
          chain.doFilter(request, response); // 다음 필터 or 요청 처리
          System.out.println("응답 반환 - Filter 실행");
      }
  }
  ```

  ---

  ## 4. Spring Interceptor 예제

  ```java
  @Component
  public class CustomInterceptor implements HandlerInterceptor {
      @Override
      public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) {
          System.out.println("Controller 실행 전 - Interceptor");
          return true; // false 반환 시 Controller 실행 X
      }

      @Override
      public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) {
          System.out.println("Controller 실행 후 - Interceptor");
      }
  }
  ```

  ```java
  @Configuration
  public class WebConfig implements WebMvcConfigurer {
      @Override
      public void addInterceptors(InterceptorRegistry registry) {
          registry.addInterceptor(new CustomInterceptor()).addPathPatterns("/api/**");
      }
  }
  ```

  ---

  ## 5. 언제 Filter와 Interceptor를 사용할까?

  - **Filter가 적합한 경우**
    - **인코딩 처리 (`CharacterEncodingFilter`)**
    - **보안, CORS 설정 (`CorsFilter`)**
    - **XSS, SQL Injection 방어**
    - **정적 리소스(이미지, CSS 등)까지 처리해야 하는 경우**

  - **Interceptor가 적합한 경우**
    - **로그인 체크**
    - **사용자 권한 검증**
    - **Controller 실행 전후에 공통 로직 적용**
    - **특정 API 요청을 가로채는 경우**

  ---

  ## 6. 결론

  - **Filter**는 **모든 요청을 전처리**할 때 사용 → **Spring이 아닌 Servlet 기반**  
  - **Interceptor**는 **Spring MVC의 Controller 요청을 전처리**할 때 사용  
  - **인증/보안**은 **Filter**, **로그인/권한 체크**는 **Interceptor** 활용이 일반적  

</details>

<details>
  <summary><h3>5. 스프링(Spring)과 스프링 부트(Spring Boot)의 차이</h3></summary>

  - **Spring**: Java 기반의 웹 프레임워크로, DI, AOP 등 다양한 기능 제공하지만 설정이 복잡함  
  - **Spring Boot**: Spring을 편리하게 사용할 수 있도록 만든 프레임워크로, **자동 설정**, **내장 웹 서버**, **단순한 배포** 지원  

  | 비교 항목 | Spring | Spring Boot |
  |-----------|--------|------------|
  | 설정 방식 | 수동 설정 (XML/Java) | 자동 설정 (`@SpringBootApplication`) |
  | 내장 서버 | 없음 | Tomcat, Jetty 포함 |
  | 실행 방식 | WAS 필요 | `java -jar` 실행 가능 |
  | 의존성 관리 | 직접 추가 | Starter 사용 (자동 관리) |

  - **Spring**: 세부 설정이 필요한 **대규모 프로젝트**에 적합  
  - **Spring Boot**: 빠른 개발이 필요한 **소규모 프로젝트 & MSA**에 적합  

</details>

<details>
  <summary><h3>5. AOP와 @Aspect의 동작 원리</h3></summary>

  ### 📌 AOP(Aspect-Oriented Programming)란?  
  - **핵심 비즈니스 로직과 공통 관심사를 분리**하여 **중복 코드를 제거**하는 프로그래밍 기법  
  - 예: 로깅, 트랜잭션 관리, 보안 처리 등  

  ### 🔍 @Aspect의 동작 원리  
  - **Spring AOP**는 프록시 기반으로 동작 (JDK 동적 프록시 or CGLIB)  
  - @Aspect 사용 시, **Spring 컨테이너가 자동으로 AOP 프록시 객체 생성**  
  - 프록시가 대상 객체를 감싸고 **메서드 실행 전후로 공통 로직 적용**  

  ```java
  @Aspect
  @Component
  public class LoggingAspect {

      @Before("execution(* com.example.service.*.*(..))")
      public void beforeMethod(JoinPoint joinPoint) {
          System.out.println("메서드 실행 전: " + joinPoint.getSignature().getName());
      }
  }
  ```

  ### ✅ 주요 어노테이션  
  - `@Before`: 메서드 실행 **전** 실행  
  - `@After`: 메서드 실행 **후** 실행  
  - `@Around`: 메서드 실행 **전/후** 실행 및 결과 조작 가능  
  - `@AfterReturning`: 정상 실행 후 실행  
  - `@AfterThrowing`: 예외 발생 시 실행  

</details>

# JPA

<details>
  <summary><h3>1. JPA 영속성 컨텍스트의 이점 (5가지)</h3></summary>

  **영속성 컨텍스트**는 엔티티를 1차 캐시에 저장하고 관리하는 JPA의 핵심 개념으로, 다음과 같은 이점을 제공한다.

  1. **1차 캐시**  
     - DB 조회 없이 **메모리에서 엔티티 조회** 가능 → 성능 향상  
  2. **변경 감지(Dirty Checking)**  
     - 엔티티 변경 시 자동으로 **UPDATE 쿼리 반영** → 코드 단순화  
  3. **트랜잭션을 활용한 원자적 연산**  
     - 트랜잭션 종료 시 **한 번의 Flush로 일괄 처리** → 일관성 유지  
  4. **지연 로딩(Lazy Loading) 지원**  
     - 연관 엔티티를 **필요할 때만 로딩** → 성능 최적화  
  5. **엔티티 동일성 보장**  
     - 같은 트랜잭션 내에서 동일 엔티티는 **항상 같은 인스턴스 유지**  

</details>

<details>
  <summary><h3>2. JPA Propagation 전파 단계 (REQUIRED vs REQUIRES_NEW)</h3></summary>

  **트랜잭션 전파(Propagation)**는 기존 트랜잭션이 있을 때 **새로운 트랜잭션을 어떻게 처리할지** 결정하는 옵션이다.

  1. **REQUIRED (기본값)**  
     - 기존 트랜잭션이 있으면 **그 트랜잭션을 사용**  
     - 없으면 **새로운 트랜잭션을 생성**  
     - 여러 메서드가 같은 트랜잭션을 공유 → 하나라도 실패하면 전체 롤백  

  2. **REQUIRES_NEW**  
     - **항상 새로운 트랜잭션을 생성**  
     - 기존 트랜잭션이 있더라도 **일시 정지하고 새로운 트랜잭션을 실행**  
     - 각각 독립적인 트랜잭션이므로 한 쪽이 롤백되어도 다른 쪽에는 영향 없음
     - 보통 반드시 성공해야 하는 기능에 사용
</details>

<details>
  <summary><h3>3. JPA를 사용하는 이유</h3></summary>

  JPA(Java Persistence API)는 객체와 관계형 데이터베이스를 매핑하는 ORM 기술로, 다음과 같은 이유로 사용된다.

  1. **생산성 향상**  
     - SQL을 직접 작성하지 않고 **객체 중심으로 개발 가능**  
  2. **유지보수 용이**  
     - 테이블 구조 변경 시 SQL 수정 부담 감소 (자동 매핑)  
  3. **변경 감지 & 자동 반영**  
     - 엔티티 변경 시 **자동으로 UPDATE 반영** (Dirty Checking)  
  4. **성능 최적화 기능 제공**  
     - **1차 캐시, 지연 로딩(Lazy Loading), 배치 쿼리(Batch Query)** 지원  
  5. **DB 벤더 독립성**  
     - 특정 DBMS에 종속되지 않고 **손쉽게 교체 가능**  

</details>

<details>
  <summary><h3>4. N + 1 문제와 해결 방법</h3></summary>

  ### 📌 N + 1 문제란?  
  - **하나의 쿼리 실행(N)** 후, 관련된 N개의 데이터를 조회할 때 **추가적인 쿼리(N번)** 가 실행되는 문제  
  - 즉, **총 N + 1번의 쿼리 발생**  

  ### 🔍 발생 원인  
  - JPA에서 **지연 로딩(Lazy Loading)** 을 사용할 때, **연관된 엔티티를 개별적으로 조회**하기 때문  
  - 예: `부모 엔티티` 조회 후, 각 `자식 엔티티`를 별도 쿼리로 가져오는 경우  

  ```java
  List<Parent> parents = parentRepository.findAll(); // 1번 실행
  for (Parent parent : parents) {
      System.out.println(parent.getChildren()); // N번 실행 (각 부모마다 자식 조회)
  }
  ```

  ### ✅ 해결 방법  
  1. **즉시 로딩(EAGER LOADING) 사용**  
     - `@OneToMany(fetch = FetchType.EAGER)`  
     - 하지만 **불필요한 데이터 로딩 가능성** 있음  

  2. **Fetch Join 사용 (권장)**  
     - `JOIN FETCH`를 이용해 한 번의 쿼리로 **연관된 엔티티까지 조회**  
     - 예: `@Query("SELECT p FROM Parent p JOIN FETCH p.children")`  

</details>
