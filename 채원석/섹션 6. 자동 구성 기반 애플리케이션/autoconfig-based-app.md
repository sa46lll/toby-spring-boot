# 메타 애노테이션과 합성 애노테이션
- 애노테이션에 붙은 애노테이션을 메타 애노테이션이라고 한다.
- 합성 애노테이션은 애노테이션을 한 개 이상 붙여서 만든 애노테이션을 의미한다.

# 빈 오브젝트의 역할과 구분
- 애플리케이션 로직 빈
- 애플리케이션 인프라스트럭쳐 빈
- 컨테이너 인트라스트럭쳐 

# 인프라 빈 구성 정보의 분리
- @import를 사용하면 클래스를 빈으로 등록할 수 있다.

# @Configuration과 proxyBeanMethods
- boolean proxyBeanMethods<br>
Specify whether @Bean methods should get proxied in order to enforce bean lifecycle behavior,
e.g. to return shared singleton bean instances even in case of direct @Bean method calls in user code.<br>
This feature requires method interception,
implemented through a runtime-generated CGLIB subclass which comes with limitations such as the configuration class and its methods not being allowed to declare final.<br>
The default is true, allowing for 'inter-bean references' via direct method calls within the configuration class as well as for external calls to this configuration's @Bean methods, e.g. from another configuration class.<br>
If this is not needed since each of this particular configuration's @Bean methods is self-contained and designed as a plain factory method for container use, switch this flag to false in order to avoid CGLIB subclass processing.<br>
Turning off bean method interception effectively processes @Bean methods individually like when declared on non-@Configuration classes, a.k.a. "@Bean Lite Mode" (see @Bean's javadoc).<br>
It is therefore behaviorally equivalent to removing the @Configuration stereotype.<br>

Since:<br>

5.2<br>

Default:<br>

true
