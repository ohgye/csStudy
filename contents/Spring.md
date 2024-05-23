# SPRING

**:Contents**
* Block/Non-Block
* Sync/Async
* [spring boot의 동작원리](#spring_boot의_동작원리)
* [스프링 프레임워크는 왜 생긴 것인가](#스프링_프레임워크는_왜_생긴_것인가)
* Bean이란
* Bean의 생명주기 / 소멸방법 / 초기화방법
* IOC(Inversion of Control, 제어의 역전)란
* DI(Dependency Injection, 의존성 주입)란
* AOP(Aspect Oriented Programming)란
* spring aop vs aspectj
* jdk dynamic proxy vs CGLIB(code Generator Library)
* Filter와 Interceptor 차이
* [spring bean 생명주기](#spring_bean_생명주기)
* [spring bean scope](#spring_bean_scope)
* [@compent로도 빈 설정을 할 수있는데 @service ,@repositorty를 나눠서 사용하는지]
* [@Autowird , @Resource , @inject 의 차이점](#@Autowird,@Resource,@inject의차이점)
* [spring 순환참조 해결방법](spring_순환참조_해결방법)
* [AOP가 Proxy 방식이라 발생할 수 있는 단점](AOP가_Proxy_방식이라_발생할_수_있는_단점)
* [spring @Autowired는 어떻게 동작할까](spring_@Autowired는_어떻게_동작할까)
* [lcoal Thread란])(lcoal_Thread란)


### Block/Non-Block
* Block(막다)상황
제어권이 호출자에서 실행함수로 넘어간 경우<br>
함수가 완료되기 전까지는 호출자는 제어권이 없다.<br>

* Non-Block(막다)상황
제어권이 호출자에서 함수를 실행해도(함수가 실행중이여도) 호출자에게 바로 제어권이 넘어간다.<br>


-----------------------------------------------------------------------


### Sync/Async
대상들의(제어권의 반환 / 결과값 전달) 시간이 맞줘지는가?<br>
* Sync
함수A => 함수B =><br>

제어권의 반환 =><br>
결과값 전달 =><br>

* Async
함수A =><br>
        함수B =><br>

제어권의 반환 =><br>
           결과값 전달 =><br>


-----------------------------------------------------------------------
           
           
### 스프링_프레임워크는_왜_생긴_것인가
`왜 '경량' 프레임워크인가?`<br>

초기 서버사이드 처리는 직접 쓰레드, 소켓연결 등을 개발자들이 직접 처리했고, 개발자 마다 구현하는 방법이 다 달라 협업에 불편함이 많았다.<br> 
이런 개발 표준을 잡은것이 Java Enterprise Edition. 그리고 그 안에 많은 스펙들을 담았고,<br>
개발자들은 그 스펙들을 구현하는 방법을 사용하기 시작했다. Servlet/JSP도 그 중 하나이다.<br>
그러나 이 구현방법 또한 여러가지 방법으로 나뉘게 되고, 개발자들은 또 정형화, 표준화 된 방법을 찾기 시작했다.<br> 
그래서 등장한 것이 Framework이다.<br>
많은 종류의 Framework이 등장하고 자바 진영에서는 대표적으로 EJB가 나왔지만 분산환경 처리에 특화된 EJB는 너무 무거운데다 불편한 점이 많았고,<br>
이런 EJB에 반기를 들고 탄생한 '경량화'된 Java 엔터프라이즈용 Framework이 Spring인 것이다.<br>


`왜 스프링을 사용하는가?` <br>

스프링은 Framework이고, Framework은 개발자들이 좀 더 쉽고 편리하게 애플리케이션을 개발할 수 있도록 미리 갖춰진 구조를 말한다.<br>
Framework이 없었다면 개발자들은 처음부터 끝까지 직접 모든 구조를 만들어내야 할 것이다.<br>
즉, 만들어진 프로그램의 성능은 개발자의 역량에 따라 극명히 갈리게 된다.<br>

스프링은 Application 개발에 필요한 하부 구조를 포괄적으로 제공함에 따라<br>
개발자들의 실력의 간극을 메꿔줄 수 있는 데다가 올바른 형태의 코드만 넣어준다면 일정 수준의 성능과 안정성을 보장해 줄 수 있다.<br>
그 틀과 구조 위에서 개발자들은 핵심 비즈니스 로직에만 집중할 수 있어서 생산성 또한 향상된다.<br>


정리 짱짱 잘되어 있다!<br>
cf) https://dreamingdreamer.tistory.com/125


-----------------------------------------------------------------------


### spring Di(Dependecy Injection)
>> 제어의 역행(IOC)으로 특정 객체에 필요한 다른 객체를 외부에서 결정해서 연결시키는 것. 

설정만 해준다면(applicationContext.xml) 스프링은 그 설정 정보를 참고해서 객체를 생성,관리하고 그 관계를 맺어준다.<br>
핵심은 개발자가 new 연산자 등을 통해 객체를 생성할 필요가 없다는 것이다(제어의 역행-IoC).<br>
개발자 입장에서는 스프링 컨테이너에게 그 참조변수만 일러준다면(@Autowired나 setter주입 등) 스프링이 알아서 객체를 생성해주고, 관계를 맺어준다.<br>
이를 의존성 주입(DI : dependency Injection)이라고 하며 개발자는 자신의 코드에 필요한 객체를 스프링을 통해 주입받는 구조로 코드를 작성한다. 


-----------------------------------------------------------------------


### spring AOP(Aspect Oriented Programming)
https://logical-code.tistory.com/118
관점지향프로그래밍 == 횡단관심에 따라 하는 프로그래밍

`aop 용어`<br>
* target object
    * 먼저 Target Object는 횡단기능(Advice)이 적용될 객체(Object)를 뜻한다. 
    * 이 객체는 핵심 모듈(비즈니스 클래스)이라 할 수 있다. Spring AOP에선 Advice를 받는 객체라 하여 Adviced Object라는 용어로 쓰이기도 한다.

    * Spring AOP에선 실제 적용할 객체 대신 Runtime Proxy를 사용하여 구현되기 때문에, Target Object는 항상 Proxy Object다.

* advice
    * Advice는 JoinPoint에 적용할 횡단 코드를(공통코드) 의미한다.
어떤 부가 기능 ? Before , AfterReturing , AfterThrowing , After , Around 

* join point
    * JoinPoint는 Target Object안에서 횡단기능(Advice)이 적용될 수 있는 여러 위치를 뜻한다.
어디에 적용할 것인가? 메서드 , 필드 , 객체 , 생성자등

* point cut
실제 advice가 적용될 시점 , spring aop에서는 advice가 적용될 메서드를 선정


`aop 구현 방법`<br>
* 컴파일
 J.java = > j.class 컴파일 하는 시점에 적용

* 클래스 로드시
j.class 메모리상에 올릴 때 적용

* 프록시 패턴(spring aop)
타겟클래스를 프록시 객체로 감싸서 부가기능을 제공


cf). https://gmoon92.github.io/spring/aop/2019/01/15/aspect-oriented-programming-concept.html

-----------------------------------------------------------------------

### spring aop vs aspectj
* `spring aop`<br>
    * 런타임 위빙 만 사용할 수 있다
    * 덜 강력 함 – 메서드 수준 위빙 만 지원
    * Spring 컨테이너가 관리하는 Bean에서만 구현 가능
    * AspectJ보다 훨씬 느림 
        * Runtime weaving: Aspect 가 대상 객체의 Proxy(JDK 동적 Proxy 나 CGLIB 의 Proxy)를 실행시 Weaving 된다
* `aspectj`<br>
    * 런타임때 아무것도 안한다. Aspect를 코드에 Weaving하기 위해, AspectJ compiler(ajc)라는 컴파일러를 도입한다.
    * 컨파일 시점 위빙
    * 더욱 강력 함 – 필드, 메서드, 생성자, 정적 이니셜 라이저, 최종 클래스 / 메서드 등을 엮을 수 있다
    * 모든 도메인 개체에서 구현 가능
    * 모든 포인트 컷 지원
    * 애플리케이션이 실행되기 전에 (런타임 전에) Aspect가 코드로 직접 짜여짐

-----------------------------------------------------------------------

### jdk dynamic proxy vs CGLIB(code Generator Library)
* Spring AOP는 프록시 기반으로 JDK Dynamic Proxy와 CGLIB을 활용하여 AOP 제공하고 있습니다.

* JDK Dynamic Proxy는 인터페이스를 구현하여 Proxy를 생성
* CGLib은 클래스를 상속받아 Proxy를 생성

* `성능의 차이`
    * 성능의 차이의 근본적인 이유는 CGLib은 타깃에 대한 정보를 제공 받기 때문입니다.
    * 따라서 CGLib은 제공받은 타깃 클래스에 대한 바이트 코드를 조작하여 Proxy를 생성



-----------------------------------------------------------------------


### IOC(Inversion of Control, 제어의 역전)란
IOC(Inversion of Control) : 의존 관계 주입(Dependency Injection)이라고도 하고,<br>
어떤 객체가 사용하는 의존 객체를 직접 만들어 사용하는게 아니라, 주입 받아 사용하는 방법을 말합니다.

스프링 IOC 컨테이너<br>
* BeanFactory 
=> 최상의 인터페이스

* 어플리케이션 컴포넌트의 중앙 저장소
* 빈 설정 소스로 부터 빈 정의를 읽어들이고 , 빈을 구성하고 제공합니다.

스프링 IOC 컨테이너의 역할
* 빈 인스턴스 생성
* 의존 관계 설정
* 빈 제공

빈(bean)이란<br>
* 스프링 IOC 컨테이너가 관리하는 객체
* 장점
    * 의존성 관리
    * 스코프
        * 싱글토 : 하나
        * 프로포토타입 : 매번 다른 객체
    * 라이프사이클 인터페이스


-----------------------------------------------------------------------

### Filter와 Interceptor 차이
spring mvc lifecycle와 함께 Filter와 Interceptor에 대해 읽기 편하게 정리된 사이트가 있다.
: https://velog.io/@damiano1027/Spring-Spring-MVC-Request-Lifecycle

-----------------------------------------------------------------------


### spring bean 생명주기

`BeanFactory 간단정리`<br>
1. 빈 객체 생성
2. BeanNameAware.setBeanName()
    >> <bean>의 id/name 속성에 지정된 값 전달
    * 스프링에서 관리되는 bean 내부에서 id나 name이 무엇으로 지정되어 있는지 확인하는 경우 BeanNameAware Interface를 구현한다.
    * 이때 그림의 노란색 부분처럼 bean생성과 property 의존성 주입을 완료한 이후, init method를 수행하기 전 시점에 호출된다.
    
3. BeanFactoryAware.setBeanFactory()
    >> bean객체에 bean을 관리하는 BeanFactory 객체 전달
    
4. BeanPostProcessor의 초기화 전처리
    >> 아래의 두 메서드를 적용하여 빈이 초기화 되기전 빈의 상태 조사 , 수정 , 확인등의 작업을 할 수 있습니다.
    * postProcessBeforeInitialization
    
```java
    public class ProductCheckBeanPostProcessor implements BeanPostProcessor {
    
    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName)
            throws BeansException {
        if (bean instanceof Product) {
            System.out.println();
            String productName = ((Product) bean).getName();
            System.out.println("In ProductCheckBeanPostProcessor.postProcessBeforeInitialization, processing Product: " + productName);
        }
        return bean;
    }
    
    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName)
            throws BeansException {
        if (bean instanceof Product) {
            System.out.println();
            String productName = ((Product) bean).getName();
            System.out.println("In ProductCheckBeanPostProcessor.postProcessAfterInitialization, processing Product: " + productName);
        }
        return bean;
    }
    }
```

5. 커스텀 init - method
    * @PostConstruct
    
6. InitializingBean.afterPropertiesSet()
7. BeanPostProcessor의 초기화 후처리
    >> 아래의  두 메서드를 적용하여 빈이 초기화 된 후 빈의 상태 조사 , 수정 , 확인등의 작업을 할 수 있습니다.
    * postProcessAfterInitialization
    
8. 빈 객체 사용
9. DisposableBean.destroy()
10. 커스텀 destroy - method  2_8_ii


`BeanFactory 공식문서`<br>
1. BeanNameAware's setBeanName
2. BeanClassLoaderAware's setBeanClassLoader
3. BeanFactoryAware's setBeanFactory
4. EnvironmentAware's setEnvironment
5. EmbeddedValueResolverAware's setEmbeddedValueResolver
6. ResourceLoaderAware's setResourceLoader
7. ApplicationEventPublisherAware's setApplicationEventPublisher
8. MessageSourceAware's setMessageSource
9. ApplicationContextAware's setApplicationContext
10. ServletContextAware's setServletContext
11. postProcessBeforeInitialization methods of BeanPostProcessors
12. InitializingBean's afterPropertiesSet (here!)
13. a custom init-method definition
14. postProcessAfterInitialization methods of BeanPostProcessors


-----------------------------------------------------------------------


#spring_bean_scope

|스코프|설명|
|------|---------------------------|
|singletone|Ioc 컨테이너당 빈 인스턴스 하나를 생성|
|prototype|요청할 때마다 빈 인스턴스를 새로 생성|
|request|HTTP 요청당 하나의 빈 인스턴스를 생성.(웹 어플리케이션 컨텍스트에만 해당)|
|session|HTTP 세션당 빈 인스턴스 하나를 생성.(웹 어플리케이션 컨텍스트에만 해당)|
|globalSession|전역 HTTP 세션당 빈 인스턴스 하나를 생성.(포털 어플리케이션 컨텍스트에만 해당)|



### @compent로도 빈 설정을 할 수있는데 @service ,@repositorty를 나눠서 사용하는지

> 레이어 역할을 분리하기 위해

* 컴포넌트 클래스들에 @Component를 붙일 수 있지만, @Repository, @Service, @Controller를 붙인다면  
* 도구들이 클래스들을 처리하는데 더 적합하도록 할 수 있고 관점(aspects)에 더 연관성을 부여할 수 있다.
* 스프링에서도 @Component보다는 @Repository, @Service, @Controller를 권장하고 있었던 것이었다.



### @Autowird , @Resource , @inject 의 차이점
> 3가지 모두 의존관계를 자동의 연결해주는 어노테이션입니다.

`@Autowired`<br>
* 스프링에서 지원하며
* 타입에 맞춰 연결합니다.

* @Autowired와 @Inject의 경우에도 @Qualifier을 이용하면 , 타입이외의 방법으로 연결할 수 있습니다.

```java

@Autowired
@Qualifier("chicken")
pirvate Brid penguin;

```

* Chicken 타입으로 연결되는 것을 알 수 있습니다


`@Inject`<br>
* 자바에서 지원하며
* 타입에 맞춰 연결합니다.

`@Resource`<br>
* 자바에서 지원해주며
* 이름에 맞춰 연결합니다.


### spring 순환참조 해결방법
* 순환참조란
    * 순환참조란 서로 다른 여러 빈들이 서로 물고늘어져서 계속 연결되어 있음을 의미
    * ex). Bean(A) -> Bean(B) -> Bean(A)  A는 B에서 필요한데 B는 또 A에서 필요한 상태
    * 순환참조가 발생하면 스프링은 어느 빈을 먼저 생성해야할지 결정하지 못하게되고 순환참조 오류가 발

* @Lazy

```java

@Compenet
public class BeanA {
    private BeanB beanb;
    
    @Autowired
    public BeanA(@Lazy BeanB beanb){
        this.beanb=beanb;
    }
}

```

* 생성자 주입

* 생성자를 통한 의존성 주입의 장점은 객체 생성 시점에서 순환 참조가 일어나기 때문에 스프링 애플리케이션이 실행되지 않습니다.
* (앱 구동 단계에서 오류를 찾을 수 있다.)
* 컨테이너가 빈을 생성하는 시점에서 객체생성에 사이클 관계가 생기기 때문입니다.


### AOP가 Proxy 방식이라 발생할 수 있는 단점(self invocation)

* 같은 객체의 자신의 메소드 외의 다른 메소드를 호출 시 AOP 적용되지 않는 것

* self-invocation 해결 방법
    * AopContext 이용
    * 자기 자신을 빈으로 등록 후, 메소드 호출
    * AspectJ Weaving 방식으로 변경


https://gmoon92.github.io/spring/aop/2019/04/01/spring-aop-mechanism-with-self-invocation.html

### spring @Autowired는 어떻게 동작할까

cf). https://kellis.tistory.com/70


### lcoal Thread란
* ThreadLocal은 thread-local 변수를 제공하는 클래스이다.
* 여기서 thread-local 변수란 말그대로 thread 내부에서 사용되는 지역변수를 의미한다.
* 가령 메소드에서 사용하는 변수나 데이터는 파라미터 혹은 메소드 scope 내에서 정의하고 사용하게 되는데, 
* Thread Local을 사용하게 되면, 굳이 변수를 파라미터 같은 곳에 넣지 않아도 공유 및 사용이 가능하게 된다.
* 그래서 앞서 언급한 SecurityContextHolder은 ThreadLocal을 통해 파라미터로 Principal을 주입 받지 않더라도, 
* 현재 SecurityContextHolder에 ThreadLocal로 저장된 Principal을 꺼내와 사용할 수 있게 되는 것이다.

* ThreadLocal 변수를 선언하면 각 스레드가 별도의 변수처럼 사용할 수 있다.
* 스레드가 종료되기 전까지 변수를 사용할 수 있다.
* 스레드풀을 통해 스레드를 재사용하는 경우 이전에 사용했던 값을 공유할 수 있다. (이해하고 목적에 맞게

cf). https://velog.io/@skygl/ThreadLocal