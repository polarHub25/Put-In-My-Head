## Spring DI/IoC는 어떻게 동작하나요?
>  DI ( Dependency Injection ) 
1. 객체 간의 결합도를 낮추기 위해 의존성을 외부에서 주입하는 방식으로 IoC의 구현 방식 중 하나입니다. 
2. 동작 원리 
- 객체 생성 및 의존성 관리 : Spring 컨테이너가 애플리케이션 실행 시 객체(Bean)을 생성하고 관리합니다
- 의존성 주입 : Spring 컨테이너는 생성된 객체들 간의 의존성을 설정 파일, 어노테이션, java config를 기반으로 자동으로 주입합니다
- 주입 방식 : DI는 생성자 주입, 필드 주입, 세터 주입 3가지 방식 <br>
-> 생성자 주입 : 객체 생성 시 필요한 의존성을 생성자를 통해 전달. 장점은 불변 객체를 만들수 있고, 테스트에서 Mock 주입이 용이하지만, 단점은 의존성이 많을 경우 생성자가 복잡해질수 있습니다.  <br>
-> 세터 주입 : 세터 메서드를 통해 의존성을 주입.  <br>
-> 필드 주입 : 어노테이션을 사용해 필드에 직접 의존성을 주입. 과거에 많이 사용한 방법 <br>


> IoC ( Inversion of Control )
1. 제어의 역전 개념으로 객체의 생성과 의존성 관리를 개발자가 아닌 프레임워크가 담당하는 구조로, 객체지향 설계의 핵심 원칙 중 하나로 객체간 결합도를 줄여 유지보수성을 높입니다.
2. 동작 원리 
- Bean 정의 및 등록 : 설정파일 (xml, config) 또는 어노테이션 ( @Component, @Service, @Repository, @Bean ) 을 통해 Bean을 정의 
- 컨테이너 초기화 : Spring 애플리케이션이 실행되면 IoC 컨테이너가 초기화되며, 필요한 Bean을 생성
- 의존성 주입 : IoC 컨테이너는 각 Bean 간의 의존성을 분석하고, 주입이 필요할 때 자동으로 의존성 주입 
- Bean 라이프사이클 관리 : IoC 컨테이너는 Bean의 생명주기를 관리

> IoC와 DI의 차이점은? 
- IoC는 큰 개념으로, 객체 생성과 의존성 주입의 제어권을 Spring으로 넘기는것을 의미하며, DI는 이러한 IoC를 실현하는 구체적인 방법으로, 외부에서 객체의 의존성을 주입하는 방식을 말합니다. 즉, DI는 IoC의 구현 방식 중 하나입니다. 

> Sping의 IoC 컨테이너는 Bean을 어떻게 관리하나요? 
- 설정파일, 어노테이션, Java config를 통해 Bean을 등록하고, 생성 시 의존성을 주입. 컨테이너는 이 Bean들을 싱글톤, 프로토타입 등의 다양한 스코프로 관리하며 , 애플리케이션 구동 시점에 필요한 Bean을 미리 준비


## DI 종류는 어떤것이 있고, 이들의 차이는 무엇인가요?
> 생성자 주입 (Constructor Injection) 
- 의존성을 생성자를 통해 주입하는 방식. 가장 권장되는 방법.
- 생성자에 @Autowired 어노테이션 추가 
- 필수적인 의존성을 명시적으로 제공하며, 불변성 보장
  
> 세터 주입 (Setter Injection)
- 클래스의 세터 메서드를 통해 의존성을 주입하는 방식.
- setter Property에 @Autowired 어노테이션 추가
- 선택적인 의존성에 대해 유연함을 제공하나, 객체가 완전히 초기화되기 전에 사용될 위험이 존재
  
> 필드 주입 (Field Injection)
- 클래스의 필드에 직접 의존성을 주입하는 방식.
- 필드에 대해서 @Autowired 어노테이션 추가
- 코드량이 적고 간결하지만, 테스트와 재사용성의 측면에서 단점이 존재 
- 현재는 좋은 방식이 아니라는 의견이 있어서 테스트 코드 이외에는 잘 사용하지 않고, 인텔리제이에서도 not recommend라고 뜸

> 왜 생성자 주입을 권장하나요?
- 객체를 생성할 때, 생성자에서 의존성이 필요한 파라미터가 주어진다면, 의존성이 주입되지 않는 객체를 생성할 수 없다는 것을 확신할 수 있습니다.
또한 스프링 컨테이너(IoC컨테이너)에서도 의존성을 주입할 Bean을 체크할 다른 로직이 필요 없어지므로 NPE를 방지할 수 있습니다.
- 의존성 주입이 필요한 객체를 final로 할 수 있어서 불변성을 가질수 있게 됩니다.  

출처 <br> 
https://github.com/Next-Squad/Interview-Question/issues/19

## Spring Bean이란 무엇인가요?
- Sping IoC 컨테이너에 의해 관리되는 객체를 말합니다. Spring 애플리케이션에서 생성되고 관리되는 모든 객체는 Spring Bean입니다. 
 Bean들은 Spring 컨테이너에 의해 생성, 주입, 관리, 소멸되며, 필요한 의존성을 자동으로 주입받아 사용됩니다. Spring 에서 모든 중요한 비즈니스 로직 객체들은 Bean으로 등록되어 IoC 컨테이너에서 관리됩니다. 

## 스프링 Bean의 생성 과정을 설명해주세요.
- Bean 등록 : 개발자가 XML 설정 파일, Java설정, 어노테이션(@Controller, @Service, @repository, @Component)을 통해 Bean을 정의하고 등록 
- Bean 인스턴스화 : IoC가 컨테이너가 애플리케이션 시작 시점에 등록된 Bean을 인스턴스화 합니다. 
- 의존성 주입 : 인스턴스화된 Bean에 필요한 의존성을 컨테이너가 주입합니다.(DI) 이 과정은 생성자 주입, 세터 주입, 필드 주입으로 이루어집니다. 
- 초기화 메서드 호출 : Bean이 초기화되며, 만약 설정된 초기화 메서드가 있다면 해당 메서드가 호출됩니다. 
- Bean 사용 : Bean은 애플리케이션 내에서 사용됩니다. 컨테이너는 애플리케이션 실행 동안 Bean을 관리합니다. 
- 소멸 메서드 호출 : 애플리케이션 종료 시점에 Bean이 소멸되며, 설정된 소멸 메서드가 호출됩니다. 

> 생성 주기 
- 객체 생성 -> 의존 설정 -> 초기화 -> 사용 -> 소멸
- 스프링 컨테이너가 초기화 될때 먼저 빈 객체를 설정 정보에 맞추어 생성하고, 의존관계를 설정한 뒤에 해당 프로세스가 완료되면 빈 객체가 지정한 메서드를 호출해서 초기화한다. 객체를 사용한 뒤 컨테이너가 종료될때 빈이 지정한 메서드를 호출해 소멸 과정을 진행한다

## 스프링 Bean의 Scope에 대해서 설명해주세요.
출처 <br> 
https://docs.spring.io/spring-framework/reference/core/beans/factory-scopes.html
https://code-lab1.tistory.com/186

> 정의
- Bean Scope는 Spring IoC컨테이너에서 Bean이 생성되고 관리되는 범위

> 종류 
1. Singleton (싱글톤)
   - 기본 스코프이며, Spring IoC 컨테이너 당 하나의 인스턴스만 생성. 애플리케이션 전체에서 동일한 객체를 공유
2. Prototype (프로토타입)
  - 요청 시마다 새로운 Bean 인스턴스를 생성. 상태가 있는 객체나 매 요청마다 새 객체가 필요한 경우에 유용
3. Request (요청 스코프)
  -  웹 애플리케이션에서 HTTP 요청 당 하나의 Bean 인스턴스를 생성하며, 요청이 끝나면 소멸
4. Session (세션 스코프)
  - HTTP 세션 당 하나의 Bean 인스턴스를 생성하고, 세션이 종료되면 소멸. 사용자의 로근 세션 동안 상태를 유지하는데 사용 
5. Application (애플리케이션 스코프)
  - 서블릿 컨텍스트의 생명주기와 동일한 범위를 가짐. 애플리케이션 전역에서 공유되는 객체를 관리할 때 사용 
6. WebSocket
  - WebSocket 세션당 하나의 Bean 인스턴스를 생성. 실시간 통신을 처리할 때 사용

> 웹 애플리케이션에서 Request 스코프와 Session 스코프의 차이점은 무엇인가요?
- Request 스코프는 HTTP 요청 당 하나의 Bean을 생성하고, Session 스코프는 HTTP 세션당 하나의 Bean을 생성합니다.

## IoC 컨테이너의 역할은 무엇이 있을까요?
> 정의
- Spring의 핵심 요소로, 객체의 생성 및 관리, 의존성 주입, 생명주기 제어 등을 담당. IoC 컨테이너는 개발자가 객체의 생성과 관리를 직접 하지 않도록 해주며 객체간의 결합도를 낮추어 애플리케이션의 유연성과 테스트 용이성을 높이는 역할 

> 역할
1. 객체의 생성 및 관리
   - IoC 컨테이너는 애플리케이션에 필요한 객체(Bean)을 생성하고, 관리. 개발자가 객체를 직접 생성하는 대신 Spring 컨테이너가 대신 처리
2. 의존성 주입 (DI)
   -  IoC 컨테이너는 객체 간의 의존성을 설정 파일이나 어노테이션 기반으로 주입. 이를 통해 객체 간의 결합도를 낮추고, 유연한 설계 가능
3. Bean 등록 및 검색
   - 설정된 Bean들을 관리하며, 필요할 때 Bean을 검색하고 제공.
4. Bean의 생명주기 관리
   - Bean의 생성, 초기화, 소멸까지의 전 과정을 관리. 초기화 메서드(@PostConstruct)와 소멸 메서드(@PreDestroy)를 통해 Bean의 생명주기 중 특정 작업을 수행
5. Bean 스코프 관리
   - 각 Bean의 스코프를 관리
6. AOP(Aspect-Oriented Programming) 지원
   - AOP를 지원하며, 로깅, 트랜잭션 관리 등 횡단 관심사를 별도의 코드로 분리하여 관리

> IoC 컨테이너가 Bean을 어떻게 관리하나요?
- IoC 컨테이너는 설정 파일, 어노테이션 또는 Java Config를 기반으로 Bean을 생성하고, 의존성을 주입한 후 생명주기를 관리

 > Spring IoC 컨테이너의 두 가지 주요 구현체는 무엇인가요?
- 주요 구현체로는 BeanFactory와 ApplicationContext가 있습니다. ApplicationContext는 더 많은 기능을 제공하며, 대부분의 Spring 애플리케이션에서 사용

> BeanFactory와 ApplicationContext의 차이점은 무엇인가요?
-  BeanFactory는 기본적인 DI 기능만 제공하는 반면, ApplicationContext는 추가적으로 AOP, 이벤트 리스닝, 메시지 리소스 처리 등의 기능을 제공

> Spring에서 Bean의 생명주기를 관리하기 위한 어노테이션은 무엇인가요?
- @PostConstruct와 @PreDestroy 어노테이션을 사용하여 Bean의 초기화 및 소멸 시점을 제어

> IoC 컨테이너에서 Bean의 스코프를 설정하는 방법은 무엇인가요?
- @Scope 어노테이션을 사용하여 Bean의 스코프를 설정할 수 있습니다. 기본 스코프는 싱글톤(Singleton)

> Spring IoC 컨테이너에서 AOP를 어떻게 지원하나요?
- IoC 컨테이너는 AspectJ와 같은 AOP 프레임워크와 통합되어 횡단 관심사를 처리합니다. 이를 통해 트랜잭션, 로깅 등 공통 기능을 모듈화


## Autowiring 과정에 대해서 설명해주세요.
> 정의
- Spring에서 의존성 주입(DI)를 자동으로 처리하는 방법
- Spring 컨테이너가 @Autowired, @Inject, @Resource 등의 어노테이션을 사용해 필요한 의존성을 자동으로 주입

> 주입 방식 
- 타입(Type) 기준 주입: @Autowired를 통해 Bean을 타입 기준으로 주입. 동일한 타입의 Bean이 여러 개 있을 경우, @Qualifier를 사용해 특정 Bean을 지정할 수 있음
- 생성자 주입: 생성자에 @Autowired를 사용해 의존성을 주입. 최근에는 생성자 주입이 권장.
- 필드 주입: 필드에 직접 @Autowired를 사용해 주입
- 세터 주입: 세터 메서드에 @Autowired를 사용해 주입
  
> 과정
- Spring 컨테이너는 애플리케이션 구동 시, @Autowired가 지정된 필드, 생성자, 세터 메서드를 스캔
- 해당 필드나 메서드의 타입에 맞는 Bean을 검색하여 주입
- 만약 주입할 수 있는 Bean이 없다면 예외를 발생시키거나, required=false 설정으로 예외를 무시

> @Autowired를 사용할 때 타입 충돌이 발생하면 어떻게 해결하나요?
- 타입 충돌이 발생할 때는 @Qualifier 어노테이션을 사용해 특정 Bean을 명시적으로 지정해 주입할 수 있습니다. 예를 들어, 동일한 타입의 Bean이 여러 개 있을 경우, @Qualifier("beanName")을 사용하여 원하는 Bean을 선택합니다.

> 필드 주입과 생성자 주입의 장단점을 설명해 주세요.
- 생성자 주입은 불변성과 테스트의 용이성을 보장하며, 필수 의존성을 강제할 수 있습니다. 반면 필드 주입은 코드가 간결하지만, 테스트에서 Mock 주입이 어려워 유지보수가 어렵습니다. 일반적으로 생성자 주입이 권장됩니다.

> @Autowired와 @Inject의 차이점은 무엇인가요?
- @Autowired는 Spring의 고유 어노테이션이며, @Inject는 Java 표준 JSR-330 어노테이션입니다. 둘 다 유사한 기능을 하지만, @Autowired는 required=false 속성을 통해 주입이 선택적일 수 있습니다.



## Spring Web MVC의 Dispatcher Servlet의 동작 원리에 대해서 간단히 설명해주세요.
출처 <br> 
https://github.com/Next-Squad/Interview-Question/issues/48
https://mangkyu.tistory.com/18

> 정의
- Spring Web MVC에서 요청을 처리하는 핵심 구성 요소
- 프론트 컨트롤러 패턴을 따르며, 클라이언트로부터의 모든 요청을 받아 적절한 컨트롤러로 전달하고, 응답을 반환
- 
> 동작 과정
1. Client 요청을 DispatcherServlet이 받음
2. DispatcherServlet은 요청 정보를 통해 요청을 처리할 Controller를 찾음
3. HandlerMapping에서 요청을 처리할 Controller를 검색
4. DispatcherServlet은 HandlerAdapter를 통해 검색된 Controller로 요청을 전달
5. 이후에 Controller는 서비스를 호출하고, 개발자가 작성한 비지니스 로직 진행
6. 처리된 비지니스 로직의 반환값을 Controller가 반환
7. HandlerAdapter는 Controller로부터 받은 응답을 DispatcherServlet으로 돌려줌
   - Controller가 ResponseEntity를 반환하면 HttpEntityMethodProcessor가 MessageConverter를 사용해 응답 객체를 직렬화하고 응답 상태(HttpStatus)를 설정
  - Controller가 View 이름을 반환하면 ViewResolver를 통해 View를 반환
8. 서버의 응답을 Client로 반환
  - 응답이 데이터라면 그대로 반환
  - 응답이 화면이라면 View의 이름에 맞는 View를 찾아서 ViewResolver가 적절한 화면을 반환

> DispatcherServlet의 역할은 무엇인가요?
- DispatcherServlet은 Spring MVC에서 모든 HTTP 요청을 받아들이고, 이를 적절한 컨트롤러에 전달해 처리한 뒤 결과를 클라이언트에게 반환하는 프론트 컨트롤러입니다.

> HandlerMapping과 HandlerAdapter의 역할을 설명해 주세요.
- HandlerMapping은 요청 URI에 따라 적절한 컨트롤러를 찾는 역할을 하고, HandlerAdapter는 해당 컨트롤러를 호출해 요청을 처리하는 어댑터 역할을 합니다.

> DispatcherServlet이 없는 Spring 애플리케이션이 가능한가요?
- 네. Spring Web MVC가 아닌 순수한 Spring 애플리케이션에서는 DispatcherServlet이 필요하지 않으며, 대신 다른 방식으로 요청을 처리할 수 있습니다.

> Servlet에 대해서 설명해주세요.
- 클라이언트의 요청을 처리하고, 그 결과를 반환하는 Servlet 클래스의 구현 규칙을 지킨 자바 웹 프로그래밍 기술
- 클라이언트의 요청에 대해 동적으로 작동하는 웹 어플리케이션 컴푸넌트

## 프론트 컨트롤러 패턴이란 무엇인가요?
> 정의
- 웹 애플리케이션의 진입 지점을 하나로 통합하는 디자인 패턴. 모든 요청이 하나의 중앙 컨트롤러(프론트 컨트롤러)를 통해 처리되고, 이후 필요한 컨트롤러나 뷰로 요청이 전달. Spring의 DispatcherServlet이 이 패턴.

> 장점 
- 중앙 집중화된 요청 처리
- 공통 작업(인증, 로깅, 예외 처리 등)을 한 곳에서 처리 가능
- 애플리케이션 구조를 단순화

> 프론트 컨트롤러 패턴을 사용하는 이유는 무엇인가요?
- 프론트 컨트롤러 패턴을 사용하면 모든 요청을 하나의 중앙 컨트롤러에서 처리하므로, 공통 기능(예: 인증, 로깅)을 일관성 있게 관리할 수 있습니다.

> 프론트 컨트롤러 패턴과 관련된 Spring 구성 요소는 무엇인가요?
- Spring에서 프론트 컨트롤러 패턴을 구현한 대표적인 구성 요소는 DispatcherServlet입니다. 이 서블릿이 모든 HTTP 요청을 받아 컨트롤러에 전달합니다.

> 프론트 컨트롤러 패턴을 구현하지 않은 경우 발생할 수 있는 문제는 무엇인가요?
- 요청을 개별 컨트롤러에서 직접 처리하면 코드 중복이 발생하고, 공통 기능을 관리하기 어려워집니다. 또한 유지보수성이 떨어지며 애플리케이션의 복잡도가 증가할 수 있습니다.

## Servlet Filter와 Spring Interceptor의 차이는 무엇인가요?
> 차이점
- Servlet Filter와 Spring Interceptor는 요청과 응답을 가로채는 데 사용되지만, 서로 다른 레벨에서 동작
  
> Servlet Filter
- Dispatcher Servlet에 요청이 전달되기 전/후에 url 패턴에 맞는 모든 요청에 대해 부가작업을 처리할 수 있는 기능을 제공
- 스프링 밖에서 처리 즉, 스프링 컨테이너가 아닌 톰캣과 같은 웹 컨테이너(서블릿 컨테이너)에 의해 관리
- 사용 방법 : javax.servlet의 Filter 인터페이스 구현 ( init, doFilter, destroy ) 
- 용도 : 공통된 보안 및 인증/인가 관련 작업, 모든 요청에 대한 로깅, 이미지/데이터 압축 및 문자열 인코딩, Spring과 분리되어야하는 기능
- ex) SpringSecurity

> Spring Interceptor
- Spring이 제공하는 기술, Dispatcher Servlet이 컨트롤러를 호출하기 전과 후에 요청과 응답을 참조하거나 가공할 수 있는 기능 제
- 스프링 컨텍스트에서 동작
- 사용 방법 :  org.springframework.web.servlet의 HandlerInterceptor 인터페이스를 구현(implements) ( preHandle, postHandle, afterCompletion )
- 용도 : 세부적인 보안 및 인증/인가 공통 작업, API 호출에 대한 로깅, Controller로 넘겨주는 정보의 가공

> Servlet Filter와 Spring Interceptor 중 어느 것을 사용해야 할지 결정하는 기준은 무엇인가요?
- 전역적인 요청 처리나 리소스 관리가 필요하다면 Servlet Filter를 사용하고, Spring MVC의 컨트롤러 요청 전후 처리라면 Spring Interceptor를 사용합니다.
> Spring에서 Filter와 Interceptor를 함께 사용할 수 있나요?
- 네, 가능합니다. Filter는 서블릿 레벨에서, Interceptor는 Spring MVC 레벨에서 동작하므로, 둘을 함께 사용하여 요청을 여러 단계에서 처리할 수 있습니다.
> Spring Interceptor에서 preHandle, postHandle, afterCompletion의 차이점은 무엇인가요?
- preHandle은 컨트롤러 실행 전, postHandle은 컨트롤러 실행 후, afterCompletion은 View 렌더링 후에 호출됩니다.

## Spring에서 CORS 에러를 해결하기 위한 방법을 설명해주세요.
- CORS(Cross-Origin Resource Sharing) 에러는 클라이언트가 다른 도메인에서 리소스를 요청할 때 발생
  > 해결 방법
  1. @CrossOrigin 어노테이션을 사용하여 특정 컨트롤러나 메서드에서 CORS 정책을 설정
  ``` java
  @CrossOrigin(origins = "http://example.com", allowedHeaders = "*", allowCredentials = "true")
  @GetMapping("/api/data")
  public ResponseEntity<String> getData() {
      return ResponseEntity.ok("data");
  }
  ```
  2. WebMvcConfigurer를 구현하여 전역적으로 CORS 설정을 관리
  ``` java
  @Configuration
  public class WebConfig implements WebMvcConfigurer {
      @Override
      public void addCorsMappings(CorsRegistry registry) {
          registry.addMapping("/**")
                  .allowedOrigins("http://example.com")
                  .allowedMethods("GET", "POST");
      }
  }
  ```

  3. Spring Security 설정에 CORS를 추가하여 보안 설정과 함께 적용
  ``` java
  @Configuration
  public class SecurityConfig extends WebSecurityConfigurerAdapter {
      @Override
      protected void configure(HttpSecurity http) throws Exception {
          http.cors()
         .and()
         .csrf().disable() // 필요에 따라 CSRF 비활성화
         .authorizeRequests()
         .anyRequest().authenticated();
      }
  }

  ```

> CORS 에러가 발생하는 원인은 무엇인가요?
- CORS 에러는 클라이언트가 다른 도메인에서 서버 자원을 요청할 때, 서버가 그 도메인을 허용하지 않을 경우 발생합니다. 이는 보안 상의 이유로 브라우저가 차단하기 때문입니다.
> Spring Security 설정에서 CORS를 처리하는 방법은 무엇인가요?
- Spring Security에서는 HttpSecurity.cors()를 사용해 전역적인 CORS 설정을 할 수 있습니다. 추가적으로 WebMvcConfigurer를 통해 세부 설정을 제어할 수 있습니다.
> @CrossOrigin 어노테이션을 사용할 때 주의할 점은 무엇인가요?
- @CrossOrigin 어노테이션은 특정 컨트롤러나 메서드에만 적용되므로, 전체 애플리케이션에 적용할 때는 WebMvcConfigurer를 사용하는 것이 좋습니다.


## Bean/Component 어노테이션에 대해서 설명해주시고, 둘의 차이점에 대해 설명해주세요.
- @Bean과 @Component는 모두 Spring에서 Bean을 등록하기 위한 어노테이션이지만, 사용하는 방식과 목적이 다름.

> @Bean
- 외부 라이브러리들을 Bean으로 등록하고 싶은 경우 사용
- 개발자가 생성한 인스턴스를 spring에게 Bean으로 관리해 달라고 요청하는 경우
- 1개 이상의 @Bean을 제공하는 클래스의 경우 반드시 @Configuration을 명시해 주어야 싱글톤이 보장
- 매소드 레벨에서 선언

> @Component
- 개발자가 직접 컨트롤이 가능한 class 경우 사용
- spring이 직접 인스턴스를 생성하여 Bean으로 등록하도록 하는 경우
- @Component는 @Service, @Repository, @Controller 등으로 확장
- 클래스 레벨에서 선언

> 차이점
- @Bean은 수동으로 Bean을 등록할 때 사용되며, 개발자가 Bean의 생성을 완전히 제어
- @Component는 자동 스캔을 통해 Bean을 등록하며, 개발자는 클래스에 어노테이션만 추가
  
> @Component와 @Bean의 사용 시점은 언제인가요?
- @Component는 클래스 수준에서 객체를 Bean으로 등록할 때 사용하고, @Bean은 개발자가 특정 메서드를 통해 직접 Bean을 생성하여 등록할 때 사용합니다.

> @Bean을 사용하는 이유는 무엇인가요?
- @Bean은 복잡한 객체 생성이나 외부 라이브러리 객체를 Spring 컨테이너에 등록해야 할 때 유용합니다. 이를 통해 수동으로 Bean을 설정하고 관리할 수 있습니다.

> @Component, @Bean 스이 이루어지지 않을 때, 이를 해결하는 방법은 무엇인가요?
1. @Component 스캔이 되지 않을 때
- 원인 : 주로 스캔 대상 패키지가 @ComponentScan에 포함되지 않았을 경우 
- 해결 방안 : @ComponentScan을 사용해 대상 패키지를 명시적으로 설정
<br> 
2. @Bean 스캔이 되지 않을 때
- 원인 : @Configuration 클래스가 Spring 컨텍스트에서 인식되지 않거나, 특정 프로파일이 활성화되지 않았기 때문
- 해결 방안 : @Configuration 클래스를 확인하거나, 프로파일 설정(application.yml, application.properties)을 확인

## POJO란 무엇인가요? Spring Framework에서 POJO는 무엇이 될 수 있을까요?
> 정의
- Plain old java object
- 특정 프레임워크, 라이브러리, 규약 등에 종속되지 않는 순수한 자바 객체

> 특징
- 특정 라이브러리나 프레임워크에 종속되지 않고, 비즈니스 로직을 구현할때 자유롭게 사용가능하며, 특정 API나 프레임워크에 대한 의존성이 없기 때문에 다른 환경에서도 쉽게 활용이 가능
  
> Spring Framework에서 POJO는 무엇이 될 수 있을까요?
- 서비스 클래스 : @Service 어노테이션을 사용한 클래스. 특정 인터페이스를 구현하거나, 특정 프레임워크 규칙을 따르지 않고 순수 자바 객체로 구성
- 엔티티 클래스 : 데이터베이스와 매핑되는 엔티티 클래스(@Entity). 단순히 속성과 게터/세터 메서드를 가진 순수 자바 객체
- 컨트롤러 클래스 : Spring mvc 에서 @Controller, @RestController로 정의된 클래스. 특정 프레임워크에 종속되지 않은 채 비즈니스 로직을 처리

>  POJO와 Spring Bean의 차이점은 무엇인가요?
- POJO는 특정 프레임워크에 의존하지 않는 순수한 자바 객체. Spring Bean은 Spring 컨테이너에 의해 관리되는 객체로, POJO일 수도 있지만 Spring의 관리 하에 생명주기, 의존성 주입 등이 추가적으로 적용

> Spring Framework는 POJO 기반으로 설계되었다고 하는데, POJO가 특정 프레임워크에 의존하지 않는 이유는 무엇인가요?
- POJO는 특정 인터페이스나 상속을 강제하지 않으며, Spring은 POJO를 관리하기 위해 IoC 컨테이너를 사용. POJO는 프레임워크에 종속되지 않고 순수 자바 객체로 작성되어, 다양한 환경에서도 독립적으로 사용

> POJO와 spring 어노테이션의 관계
- Spring이 POJO 기반이라고 하는 이유는, 어노테이션을 통해 Spring이 관리하더라도, 비즈니스 로직은 특정 프레임워크에 종속되지 않고 자유롭게 구현할 수 있기 때문
- Spring 어노테이션을 사용하면 해당 클래스는 Spring에 의존하게 됨. 하지만, 이 의존성은 주로 Spring 컨테이너와 관련된 부분이며, 비즈니스 로직 자체는 여전히 순수 자바 객체로 작성

## Spring Web MVC에서 요청 마다 Thread가 생성되어 Controller를 통해 요청을 수행할텐데, 어떻게 1개의 Controller만 생성될 수 있을까요?
- Spring web MVC에서 컨트롤러는 기본적으로 싱글톤 스코프 (힙 메모리에 저장)이며, spring container가 해당 컨트롤러 빈을 한번만 생성합니다. 이후에 모든 요청에 대해서는 동일한 컨트롤러 인스턴스를 사용하여 처리되며, 상태 없는(stateless) 설계로 인해 여러 스레드가 동시에 접근해도 안전하게 동작합니다. 이는 인스턴스 변수를 사용하지 않고 로컬 변수를 사용해 데이터를 처리하기 때문입니다. 즉, 여러 요청이 동일한 컨트롤러 인스턴스를 공유하지만, 각 요청에 대해 별도의 스레드가 동작하기 때문에 1개의 컨트롤러로 처리가 가능합니다. 

> 컨트롤러가 상태를 가지지 않는(stateless) 방식으로 설계된다는 것은 무엇을 의미하나요?
- 모든 요청 데이터는 로컬 변수로 처리되며, 메서드 내에서만 존재하므로 각 요청이 독립적으로 처리될수있도록 설계된 방식입니다.

## Spring WEB MVC의 근간에는 Java Servlet 이 있는데요. Spring 은 Servlet을 어떻게 구성해서 이를 구현했을까요?
- Spring Web MVC는 Java servlet을 기반으로 동작하며, DispatcherServlet이 있습니다. DispatcherServlet은 Java Servlet의 HttpServlet을 상속받아 모든 요청을 중앙에서 처리하는 프론트 컨트롤러 역할을 수행합니다. 요청이 들어오면 DispatcherServlet은 HandlerMapping을 통해 적절한 컨트롤러를 찾아 호출하고, HandlerAdapter를 통해 컨트롤러 메서드를 실행합니다. 이후 반환된 결과를 ViewResolver를 통해 View로 변환하고 응답을 생성합니다. Spring은 이런 구조를 통해 Servlet Api를 확장해서 구현하였습니다. 

## Filter는 Servlet의 스펙이고, Interceptor는 Spring MVC의 스펙입니다. Spring Application에서 Filter와 Interceptor를 통해 예외를 처리할 경우 어떻게 해야 할까요?
> Filter
-  doFilter메서드에서 try-catch를 사용하여 예외 처리.
-  HttpServletResponse 상태코드를 설정하여 Client에 오류 메시지 전달

> Interceptor
- preHandle, postHandle 에서 발생한 예외는 @ControllerAdvice에서 처리
- afterCompletion에서는 뷰 렌더링(클라이언트로 전송된 이후)까지 완료된 후에 호출이므로, @ControllerAdvice로 처리되지않고 주로 로깅 용도로 활용. 실제 예외 발생시 로그만 남기고 추가적인 처리 없이 종료 <br>
  ex) db 커넥션, 파일 핸들러, 외부 api 호출 후 정리 작업 등 

> filter와 interceptor 중 예외 처리를 위해 어떤 것을 선택해야 하나요?
- 예외 처리가 spring mvc의 컨트롤러와 관련이 있거나 요청 흐름 중 발생할 가능성이 크다면 interceptor을 사용하는 것이 적합하고, 인증, 로깅, 필터링 등 전역적이고 독립적인 예외 처리가 필요하다면, filter가 적합합니다. 

## Spring Application을 구동할 때 메서드를 실행시키는 방법에 대해 설명해주세요.
> @PostConstruct
- Bean이 초기화된 후 호출, 애플리케이션 구동 시점에 해당 메서드를 자동으로 실행 (주로 초기화 작업 처리시 사용)
> CommandLineRunner 인터페이스
- 애플리케이션 구동 후 실행되는 코드를 정의 할수 있음
- run(String... args) 메서드를 구현하여 코드 작성
> ApplicationRunner 인터페이스
- CommandLineRunner와 유사하지만, 더 구조화된 ApplicationArguments 객체를 통해 인자를 전달받아 사용 가능
> @EventListener
- spring에서 제공하는 이벤트 시스템을 이용해 애플리케이션이 구동될때 실행할 코드 작성 가능

>실무에서 비동기 초기화 작업을 애플리케이션 구동 시 처리해야 했던 경험이 있나요? 그런 작업을 어떤 방식으로 처리했는지 설명해주세요.

## 의존성과 설정값을 생성자 인자로 주입해야 하는 이유에 대해 설명해주세요.
- 객체의 불변성 확보 : 생성자 주입을 통해 변경의 가능성을 배제하고 불변성 보장
- 컴파일 시점에 객체를 주입받아 테스트 코드 작성이 가능하며, 주입하는 객체가 null인 경우 컴파일 시점에 오류 발견 가능
- 필드 객체에 final 키워드를 사용할 수 있고, 컴파일 시점에 누락된 의존성 확인 가능
-  애플리케이션 구동 시점(객체 생성 시점)에 순환 참조 에러 방지 가능

> 생성자 주입을 사용할 때, 빈의 초기화 순서는 어떻게 보장되나요?
- 의존성 주입 순서를 보장하기 위해 빈 간의 의존성을 분석한 후 올바른 순서대로 빈을 초기화합니다. 즉, A 빈이 B 빈을 의존할 때, 스프링은 먼저 B 빈을 초기화한 후 A 빈을 초기화합니다. 이를 통해 순환 참조 문제를 방지하고, 초기화 순서를 보장합니다.
> 빈 초기화 순서 분석 과정
- 빈 정의 스캑 -> 의존성 그래프 생성 -> 의존성 주입 방식 분석 -> 빈 초기화 및 콜백 메서드 실행
# JPA

## JPA 영속성 컨텍스트의 이점(5가지)을 설명해주세요.
> JPA 영속성 컨텍스트
- 엔티티를 영구 저장하는 환경. 애플리케이션과 데이터베이스 사이에서 객체를 보관하는 가상의 데이터베이스 역할

> 이점 
1. 1차 캐시
- 1차 캐시에 엔티티를 저장하여 같은 트랜잭션 내에서 동일한 엔티티 조회시에 db 재조회를 하지않고 캐시에서 가져옵니다. db 접근을 줄여 성능을 향상
  
2. 동일성 보장
- 동일한 영속성 컨텍스트 내에서 조회된 엔티티는 동일한 객체
  
3. 변경 감지( Dirty Checking )
-  트랜잭션 종료 전 영속성 컨텍스트 내의 엔티티와 스냅샷을 비교하여 변경된 내용을 감지 후 update 쿼리를 생성해서 쓰기 지연 sql 저장소에 저장후 플러시( 영속성 컨텍스트의 변경 내용을 DB에 반영 )
  
4. 쓰기 지연
-   트랜잭션을 커밋하기 직전까지 내부 쿼리 저장소에 insert sql을 모아둔 후 커밋시에 모아둔 쿼리를 DB에 보내는것
  
5. 지연 로딩
- 연관된 엔티티를 즉시 조회하지 않고, 프록시 객체로만 로딩되고, 해당 엔티티가 실제로 필요할 때 db에서 조회하는 방식

>  1차 캐시는 언제 초기화되나요?
- 1차 캐시는 트랜잭션 범위 내에서 유지되며, 트랜잭션이 종료되면 영속성 컨텍스트와 함께 초기화됩니다. 새로운 트랜잭션이 시작되면 새로운 영속성 컨텍스트가 생성되고, 이때 새로운 1차 캐시가 관리됩니다.                                                          
## JPA Propagation 전파단계를 설명해주세요.
> JPA Propagation
- 트랜잭션 동작 도중 다른 트랜잭션을 호출하는 상황에 선택할 수 있는 옵션 (@Transactional)
  
> 전파단계
- REQUIRED: 현재 트랜잭션이 있으면 사용, 없으면 새로 생성 (기본값).
- REQUIRES_NEW: 무조건 새로운 트랜잭션 생성. 기존의 트랜잭션은 보류
- SUPPORTS: 트랜잭션이 있으면 사용, 없으면 트랜잭션 없이 실행.
- NOT_SUPPORTED: 트랜잭션이 있으면 일시 중단하고, 트랜잭션 없이 실행.
- MANDATORY: 기존 트랜잭션이 반드시 있어야 하며, 없으면 예외 발생.
- NEVER: 트랜잭션이 있으면 예외 발생, 없으면 트랜잭션 없이 실행.
- NESTED: 현재 트랜잭션 안에서 중첩된 트랜잭션으로 실행.

## JPA를 쓴다면 그 이유에 대해서 설명해주세요.
> 정의
- JPA(Java Persistence API)는 자바 진영의 ORM 기술 표준.
- 자바 애플리케이션에서 관계형 데이터베이스를 사용하는 방식을 정의한 인터페이스
  
> 사용 이유
- 객체지행적인 프로그래밍이 가능하고, 데이터베이스 독립성을 제공합니다. 개발자는 객체 모델에 집중하여 코드 작성이 가능하며, JPA가 자동으로 SQL을 생성함으로써 생산성을 높입니다. DB 변경시 큰 수정없이 유지보수가 가능하고, 다양한 최적화 기능을 통해 효율적인 데이터 처리가 가능합니다.

> JPA와 Hibernate의 차이점은 무엇인가요?
- JPA는 자바 표준 명세로, 특정 구현체가 아닌 인터페이스의 집합입니다. Hibernate는 JPA를 구현한 ORM 프레임워크로, JPA의 표준 기능 외에도 다양한 확장 기능을 제공합니다. JPA는 인터페이스, Hibernate는 그 구현체라고 이해할 수 있습니다.

## N + 1 문제는 무엇이고 이것이 발생하는 이유와 이를 해결하는 방법을 설명해주세요.
> N+1 문제 발생이유
- JPA 같은 ORM에서 발생하는 성능 문제로, 연관 관계가 설정된 엔티티를 조회할 경우 연관된 데이터 수만큼 연관관계의 조회 쿼리가 추가로 발생하는 현상
  
> 해결 방법
1. join fetch 사용
- 조회 시 바로 가져오고 싶은 엔티티 필드를 지정하는것 (join fetch a.subjects)
- ex ) @Query("select a from Academy a join fetch a.subjects s join fetch s.teacher")
- inner join
- 불필요한 쿼리문이 추가되는 단점 존재

2. @EntityGraph
- @EntityGraph의 attributePaths에 쿼리 수행시 바로 가져올 필드명을 지정 @EntityGraph(attributePaths = "members")
- outer join 

> N+1 문제를 해결하기 위한 @EntityGraph와 JPQL의 JOIN FETCH의 장단점은 무엇인가요?
- @EntityGraph는 코드 내에서 쿼리를 직접 작성하지 않고도 간단히 설정할 수 있어 가독성이 높고 유지보수가 용이합니다. 반면, JPQL의 JOIN FETCH는 복잡한 조건이나 동적 쿼리를 사용할 때 더 유연하게 동작합니다. @EntityGraph는 간단한 쿼리에 적합하고, 복잡한 쿼리에서는 JPQL을 선호합니다.

> 지연 로딩과 즉시 로딩을 혼용할 때 N+1 문제가 발생할 수 있는 상황을 설명해보세요.
- 지연 로딩과 즉시 로딩을 함께 사용하면, 예상치 못한 시점에 쿼리가 발생할 수 있습니다. 예를 들어, 부모 엔티티는 지연 로딩으로 설정되어 있고, 자식 엔티티는 즉시 로딩으로 설정된 경우, 부모 엔티티를 조회할 때 자식 엔티티에 대한 추가 쿼리가 발생하면서 N+1 문제가 생길 수 있습니다.














