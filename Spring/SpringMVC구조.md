# SpringMVC 구조
![springmvc구조](https://user-images.githubusercontent.com/46726709/110488901-44598f00-8132-11eb-87c4-a3a5e2844b2c.PNG)<br>

1. DispatcherServlet <br>
- 서블릿 클래스. 모든 클라이언트의 요청을 처리한다.
- Controller(Action)에게 클라이언트의 요청을 전달하고, 컨트롤러가 리턴한 결과값을 View에 전달하여 알맞은 응답을 생성하도록 한다.
2. HandlerMapping 
- 클라이언트의 요청 URL을 어떤 Controller(Action)이 처리할지 결정
- 요청 URL과 Controller 클래스의 맵핑을 관리
3. Controller(Action)
- 클라이언트의 실질적인 요청을 처리
- 처리 결과를 Model에 담아서 DispatcherServlet에 반환
4. Model
- Controller(Action)가 처리한 모델의 결과 정보를 담는다
5. ViewResolver
- Controller(Action)의 처리 결과를 생성할 뷰를 결정
- Controller가 리턴한 뷰 이름, (뷰네임)으로 실행될 JSP 경로 완성
6. View
- Controller(Action)의 처리 결과 화면, 출력 데이터를 설정




# SpringMVC 처리순서






### 참조 
[spring구조 이해및처리](https://iri-kang.tistory.com/4)<br>
[spring mvc 처리과정](https://jeong-pro.tistory.com/96)<br>
