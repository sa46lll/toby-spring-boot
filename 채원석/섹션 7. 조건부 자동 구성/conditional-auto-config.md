# 스타터와 Jetty 서버 추가
- 스프링부트는 톰캣 외에 제티와 언더토우라는 내장 서버를 제공한다.
- 제티는 was 중에서 가벼운 편에 속한다.

# @Conditional과 Condition
- @Conditional은 컴포넌트의 Bean 등록 여부에 조건을 달 수 있게 해주는 어노테이션
- value에 conditional interface 구현체를 전달한다.

# 커스톰 @Conditional
```
public class MyOnClassCondition implements Condition {
@Override
public boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
Map<String, Object> attrs = metadata.getAnnotationAttributes(ConditionalMyOnClass.class.getName());
String value = (String) attrs.get("value");
return ClassUtils.isPresent(value, context.getClassLoader());
}
}
```
- ClassUtils.isPresent() : 특정 클래스가 프로젝트에 포함되어 클래스패스에 존재하는가를 확인하는 클래스

# 스프링 부트의 @Conditional
```
@Target({ElementType.TYPE, ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface Conditional {
/**
* All {@link Condition} classes that must {@linkplain Condition#matches match}
* in order for the component to be registered.
*/
Class<? extends Condition>[] value();
}
```
