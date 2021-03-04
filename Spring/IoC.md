# IoC(Inversion Of Control) 제어역행
 ## IoC란?
  - IoC객체의 생성, 생명주기의 관리까지 모든 객체에 대한 제어권이 바뀐 것을 의미.<br>
    기존에 자바 애플리케이션을 개발할 때 자바 객체를 생성하고 서로간 의존
    관계를 연결작업에 대한 제어권은 보통 개발되는 어플리케이션에 있었다.
  - 컴포넌트 의존관계 결정, 설정 및 생명주기를 해결하기 위한 디자인 패턴
  - Servlet, EJB 등을 사용하는 경우 Servlet Container, EJB Container에게
    제어권이 넘어가서 객체의 생명주기(Life Cycle)를 Container들이 전담하게 된다.
  - Spring Framework의 중요특성

## IoC의 컨테이너
  - IoC컨테이너는 객체의 생성을 책임지고, 의존성을 관리한다
  - POJO의 생성, 초기화, 서비스, 소멸에 대한 권한을 가진다.
  - 개발자들이 직접 POJO를 생성할 수 있지만 컨테이너에 맡긴다.








### 참조
[IoC컨테이너와 DI](https://dog-developers.tistory.com/12)<br>
