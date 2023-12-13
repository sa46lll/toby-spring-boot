# environment 추상화와 프로퍼티
- profile과 properties가 제공된다.
- 프로퍼티의 경우 스프링 부트에서는 application.properties, applicatiom.xml등에서 읽어오도록 한다.

# 자동 구성에 Environment 프로퍼티 적용
- ApplicationRunner 인터페이스 구현한 람다식 혹은 오브젝트를 빈으로 등
```
@FunctionalInterface
public interface ApplicationRunner
Interface used to indicate that a bean should run when it is contained within a SpringApplication. Multiple ApplicationRunner beans can be defined within the same application context and can be ordered using the Ordered interface or @Order annotation.

Since:
1.3.0

Author:
Phillip Webb
```

# 프로퍼티 클래스의 분리
- 프로퍼티의 개수가 많아지고 복잡해지면서 별도의 클래스로 분류하는 것을 의미한다.
