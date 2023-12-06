## DI와 테스트

웹 서버에 HTTP 요청과 응답에 대한 테스트코드는 이렇게 작성할 수 있다.

```java
@Test
void hello(){
        TestRestTemplate restTemplate=new TestRestTemplate();

        ResponseEntity<String> res=restTemplate.getForEntity(
        "http://localhost:8080/hello?name={name}",String.class,"Spring");

        assertThat(res.getStatusCode()).isEqualTo(HttpStatus.OK);
        assertThat(res.getHeaders().getFirst(HttpHeaders.CONTENT_TYPE)
        .startsWith(MediaType.TEXT_PLAIN_VALUE)).isTrue();
        assertThat(res.getBody().trim()).isEqualTo("Hello Spring");
        }
```

DI는 컨테이너 없이도 테스트 코드를 작성할 때 의존 관계 주입을 이용해서 테스트를 진행할 수 있게 한다.
컨테이너 없이 테스트 코드를 작성하게 되면, 수행 속도도 매우 빨라진다.

```java
@Test
void simpleHelloService(){
        SimpleHelloService helloService=new SimpleHelloService();
        String ret=helloService.sayHello("Test");
        Assertions.assertThat(ret).isEqualTo("Hello Test");
        }
```

## DI (Dependency Injection)

컨트롤러는 서비스의 구현체에 직접 의존하지 않지만, 런타임시에는 구현체를 사용하고 있어야 하므로 의존 관계가 존재한다.
이 의존 관계는 처음 스프링 컨테이너가 뜰 때, 스프링 컨테이너가 DI의 Assembler 역할을 해서 의존 관계를 연결해준다.

잠시 Gang of Four의 객제치향 디자인 패턴 중 2가지를 살펴보자.

### Decorator 패턴

Decorator 패턴은 기존의 코드를 수정하지 않고도, 기능을 추가할 수 있게 해주는 패턴이다.
예를 들면, HelloService의 또 다른 구현체를 호출할 수 있다라는 것이다. 이것은 런타임 시에 구현체를 바꿔서 사용할 수 있다는 것을 의미한다.

![스크린샷 2023-12-06 190845](https://github.com/LeeJaeYun7/toby-spring-boot/assets/62706048/7de9ec8b-8bdd-4d96-b89d-49db9c2aec7b)


런타임시의 구조이다.

![스크린샷 2023-12-06 191020](https://github.com/LeeJaeYun7/toby-spring-boot/assets/62706048/5ddc2674-6a13-44cc-b41f-c2b9d51084c3)

만약 구현체가 하나라면, 단일 주입 후보를 자동으로 주입하게 된다. 이것을 오토와이어링이라고 한다. (Autowired)
지금은 구현체가 2개 이상이라고 하자.

```java
@Service
public class HelloDecorator implements HelloService{
    private final HelloService helloService;

    public HelloDecorator(HelloService helloService){
        this.helloService=helloService;
    }

    @Override
    public String sayHello(String name){
        return helloService.sayHello(name).toUpperCase(); // 기존의 기능을 유지하면서, 추가적인 기능을 더할 수 있다.
    }
}

```

실행하면, 스프링 컨테이너가 시작될 때, 구현체가 2개 이상이라는 것을 알게 되고, 두 개의 구현체를 주입할 수 없다는 에러가 발생한다.

![스크린샷 2023-12-06 191702](https://github.com/LeeJaeYun7/toby-spring-boot/assets/62706048/9e984a68-2309-47a1-836b-89ed6bb6591b)

구현체를 명시적으로 지정해주면, 에러가 발생하지 않는다.
xml 파일에 명시적으로 지정해주는 방법도 있고, factory 메소드를 이용해서 Java 코드로 명시적으로 지정해주는 방법도 있다. 
후보가 2개인 경우에는 우선순위를 지정해주는 방법도 있다. (Primary)

HelloDecorator에 Primary 어노테이션을 붙여주면, HelloController에서 HelloService를 주입받을 때, HelloDecorator를 주입받게 된다.
그리고, HelloDecorator는 남은 HelloSimpleService를 주입받는다. 이렇게 되면, HelloDecorator는 HelloService의 구현체를 주입받게 되는 것이다.

```java
@Service
public class HelloDecorator implements HelloService{
    private final HelloService helloService;
// ...
}
```

### Proxy 패턴

Proxy 패턴은 서버가 시작될 때 객체를 미리 생성하지 않고, 요청이 들어올 때 객체를 생성하는 패턴이다.
객체 생성이 비싼 경우에는, 이 패턴을 사용하면 성능을 향상시킬 수 있다. 최대한 지연시켜서 객체를 생성하는 것이다. (Lazy Initialization)

실제로 이미 스프링에서는 이 패턴을 사용하고 있다.
스프링 컨테이너가 시작될 때, HelloService를 구현한 객체를 생성하지 않는다. 그리고, HelloController에서 HelloService를 주입받을 때, HelloService를 구현한 객체를 생성한다.

또한, JPA에서도 사용되는 패턴이다. JPA에서는 실제로 DB에 접근하는 객체를 생성하지 않고, 프록시 객체를 생성한다. 그리고, 실제로 DB에 접근하는 객체가 필요할 때, 프록시 객체가 실제 객체를 생성한다.

