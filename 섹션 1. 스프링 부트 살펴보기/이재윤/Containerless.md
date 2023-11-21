

```
Summary

1. Containerless?
- 컨테이너가 없는? 컨테이너란?
-> 컨테이너가 필요 없다는 것은 아니고, Serverless와 유사함
-> 즉, 서버에 대한 설치, 관리 등을 개발자가 신경쓰지 않고, 서버 애플리케이션을 운영하고 배포하는 것이 가능한 것을 서버리스라고 함
-> Containerless도 그것과 비슷

2. Container?
-> 스프링은 IoC Container
-> 웹 프로그램을 개발하는 것은 서버에서 동작하면서 기능하는 여러 Component를 만드는 것임
-> Web Component는 항상 Web Client를 필요로 함  
-> Web Component의 목표는 Dynamic Content를 만드는 것임
-> Web client에게 응답으로 보내줌

- Web Component는 항상 Web Container안에 들어가 있어야 함
-> Web Container는 라이프 사이클 관리를 해줌
-> 또한, Web Container는 하나의 Web Component만 관리하지 않음
-> 회원가입, 로그인, 주문 등등
-> Web Container는 요청을 정해준 룰에 따라서 Web Component에 연결해줌(라우팅 or 매핑)

- 자바에서는 Web Component를 Servlet이라고 부름
-> Servlet을 관리해주는 Container가 Servlet Container(ex) Tomcat)


3. Spring?
- Spring Container는 Servlet Container 뒤쪽에 존재하면서, Component(=Bean)
-> Spring Container가 Servlet Container를 대체할 수는 없음
-> 자바의 표준 웹 기술을 사용하려면

- "Hello World"라도 띄우려면, Servlet Container가 무조건 떠야함
-> Servlet Container를 띄우는 것이 간단하지 않음
-> 오래된 기술이기도 하고, 다양한 설정 방법들을 요구함

- Servlet Container를 통해서 Spring Container가 호출됨
-> 전체 Servlet Container위에서 돌아가는 애플리케이션은 WAR 형식의 파일로 빌드가 되어야 함
-> 중요한 것은 폴더 구조가 중요함

- Spring Boot는 독립적인 서버 프로그램
-> 배포를 했을 때, 안되는 문제가 발생하면 해결할 줄 알아야 함
-> Servlet Container에 설정할게 굉장히 많음

- Servlet Container는 표준 스펙이고, 그것을 구현한 제품을 사용해야 함
-> 대표적인 것이 톰캣
-> 프로젝트에서 다른 종류의 Servlet Container를 쓴다면?
-> 진입 장벽이 높고, 학습 곡선이 높음

- Servlet Container가 필요하지만, 설정과 관련된 작업을 제거했으면 좋겠다.
-> Spring Container와 빈의 등록 방법을 알면 바로 사용할 수 있게 됨  


Insight
- Containerless의 의미에 대해 명확하게 이해하게 됨
- Servlet Container와 Spring Container의 차이점과 관계, 그리고 각각의 구성 요소에 대해서 명확하게 이해하게 됨 


Application
- Servlet Container, Spring Container에 대해서 더 깊게 학습하고 이해할 필요가 있다.  

```
