# Servlet

서버에서 웹페이지 등을 동적으로 생성하거나 데이터 처리를 수행하기 위해 java로 작성된 프로그램
- java 코드 안에 HTML 태그가 삽입된다.
- 클라이언트 요청을 처리하고 그 결과를 다시 클라이언트에게 전송하는 Servelt 클래스의 구현 규칙을 지킨 자바 프로그램
- 자바 코드로 구현하고 컴파일하고 배포한다.
- HTML태그를 문자열 스트림으로 처리해야한다.
- 코드가 수정되면 다시 컴파일하고 배포해야 한다.


# JSP(Java Server Pages)

HTML문서에 내부적으로 자바 문법을 삽입하는 웹페이지 스크립트 언어. <br> 
- servlet(서블릿)의 단점을 보완하고자 만든 서블릿 기반의 '서버 스크립트 기술'
- 키워드가 태그화 되어 서블릿에 비해 배우기 쉽다
- 자바코드를 <%%>태그 안에 처리해서 사용 가능하다

## Servlet과 JSP 비교
- JSP는 사용자에게 결과를 보여주는 화면(뷰)을 담당한다
- Servley은 사용자(화면)의 요청을 받아 처리하고 가공해서 결과를 사용자(화면)에게 응답하는 컨트롤러 층을 담당한다.


## Model1 Model2
- Model1 : JSP만 이용한 개발. 유지보수단계에서 단점이 많다.
- Model2 : JSP와 Servlet을 역할을 나누어 동시에 사용하여 개발하는 방식 (MVC)
> 프레젠테이션 로직과 비즈니스 로직 분리<br>
(보여지는 부분은 HTML이 중심인 JSP, 다른 자바 클래스에 데이터를 넘겨주는 부분은 자바 코드 중심의 Servlet)<br>
유지보수가 용이하다

## MVC Pattern

#### Model (Service클래스 or Java Bean)
 비즈니스 로직을 처리하는 모든것.  컨트롤러부터 특정 로직에 대한 처리요청이 들어오면 수행하고 수행결과를 컨트롤러에 반환.
 - request 나 session에 저장하기도 한다.
 - 서비스 클래스(ex.EmployeeService)또는 자바빈 또는 DTO,DAO.
 
#### View (JSP)
  클라이언트에 출력되는 화면. 처리로직을 위한 코드는 내포하지 않는다. 요청 결과의 출력 뿐만 아니라 컨트롤러에 요청을 보내는 용도로 사용
  - request  나 session에 저장된 정보를 토대로 화면 출력
  
#### Controller (servlet)
   모든 흐름제어를 맡는다. 요청이 들어오면 요청을 분석해 요청을 처리하기 위한 모델을 사용하여 처리. 모델로부터 결과를 받으면
   추가 처리를 한 후 request나 session객체에 저장하고 뷰(jsp 페이지) 선택해 forward나 redirect해 클라이언트에 출력
 
 - 분업이 되어있어 유지보수 용이하다.
 - java에 대한 깊은 이해도가 필요하다
 - 구조가 복잡하여 습득이 어렵고 작업량이 많다.


### 참조
[JSP와 Servlet(서블릿)](https://m.blog.naver.com/acornedu/221128616501) <br>
[JSP와 Servlet 왜 같이 사용하는가?](https://anster.tistory.com/128) <br>
[웹 개발을 위한 프레임워크](https://www.holaxprogramming.com/2012/12/18/java-hello-j2ee/) <br>
[프레임워크란?](https://www.castingn.com/sourcing/kkultip_detail/110) <br>


