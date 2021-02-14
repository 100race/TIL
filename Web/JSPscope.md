 
 # Scope객체
 
 JSP 페이지 이동시 값을 가져가는게 불편하다. 이를 위해서 활용하는 객체. 
 - 속성(Attribute) : 공유되는 데이터
 - 영역(Scope) : 속성을 공유할 수 있는 유효범위, 생존기간
 - 4개의 영역 범위가 존재 page, request, session, application
 
    ### scope범위
   
   page < request < session < application
 
   ### page 
   범위 : 현재 페이지
   - 하나의 JSP 페이지 내에서 지역변수처럼 사용되어 공유될 값을 저장한다.
   - 해당 페이지가 클라이언트에 서비스를 제공하는 동안에 유효.
   - 지역변수처럼 사용된다
   - forward 될 경우 사용되지 못한다.
 
   ### request
   범위 : 현재 요청이 끝날 때까지
   - http요청을 WAS가 받아서 웹 브라우저에 응답할 때 까지 변수가 유지되는 경우 사용
   - 클라이언트의 요청이 처리되는 동안 유효
   - 하나의 요청을 처리하는데 사용되는 JSP페이지 사이에서 정보를 전달하기 위해 사용
   - forward 되기전 setAttribute()로 값을 설정한 후, 전달된 값을 출력 가능. 유지됨
   ```
   //servlet 전달
   request.setAttribute("이름", 객체);
   //JSP 받기
   Object obj = request.getAttribute("이름");
   ```
   
   ### session 
   [세션이란?](https://github.com/100race/TIL/blob/main/Web/session.md)<br>
   범위 : 세션이 종료될 때 까지(로그아웃 할때까지)
   - 하나의 브라우저 당 1개의 session 객체
   - 웹 브라우저 탭 간에 세션정보 공유됨. 웹 브라우저 별로 변수가 관리되는 경우 사용
   - 한 사용자와 관련된 정보를 JSP들이 공유하기 위해서 사용. 
   - 서블릿에서는 HttpServletRequest의 getSession()을 이용해 session 객체를 얻는다.
   ex. 사용자의 로그인 정보
   ```
   request.getSession();
   ```
   
   
   ### application
   범위 : 웹 어플리케이션 종료시 까지
   - 웹 어플리케이션이 시작되고 종료될 때까지 변수가 유지되는 경우 사용
   - 모든 클라이언트가 공유할 정보를 저장. 임시 디렉토리 경로와 같은 웹 어플리케이션의 설정 정보를 주로 저장.
   ex. 블로그 방문자 수 
   ```
   request.getServletContext();
   ```
   

   
  ## scope 객체의 속성 처리 메서드
  - setAttribute(String name, Object value) <br>
   : 저장시 호출하는 메서드. 타입 상관 없다. 객체타입으로 upcasting됨
  - getAttribute(String name) <br>
   : Object 타입으로 저장된 값 반환
  - removeAttribute(String name) <br>
  - getAttributeNames() <br>
  
### 예제 코드
   ### Servlet
  ```
  @WebServlet("/scope") // 이 서블릿 페이지를 웹에서 접근할 수 있는 url
public class ScopeSerlvet extends HttpServlet {
    private static final long serialVersionUID = 1L;


    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // page는 JSP파일에서 작성 ( JSP only )

        // request
        request.setAttribute("num2", 20);

        // session
        request.getSession().setAttribute("num3", 30);

        // application
        request.getServletContext().setAttribute("num4", 40);

        RequestDispatcher rd = request.getRequestDispatcher("/WEB-INF/index.jsp");
        rd.forward(request, response);
    }

    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doGet(request, response);
    }
}
  ```
   ### JSP
  ```
  <%
    pageContext.setAttribute("num1", 10);
%>

<%@ page language="java" contentType="text/html; charset=UTF-8"
pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
</head>
<body>
    ${ pageScope.num1 } <br>
    ${ requestScope.num2 } <br>
    ${ sessionScope.num3 } <br>
    ${ applicationScope.num4 } <br>
    <hr>
    ${ num1 } <br>
    ${ num2 } <br>
    ${ num3 } <br>
    ${ num4 } <br>
</body>
</html>
```
- 첫째 방법 : scope영역 명시 후 출력하고자 하는 속성 명 작성
- 두번째 방법 : 속성 명 제대로 알고 있을 경우, 속성 명 만으로 지정

### 참조
[영역 객체와 속성](https://blog.naver.com/javaking75/140181686711, "jsp link") <br>
[scope란?](https://m.blog.naver.com/PostView.nhn?blogId=good_ray&logNo=221325440532&proxyReferer=https:%2F%2Fwww.google.com%2F, "jsp link") <br>
[객체 범위](https://victorydntmd.tistory.com/155, "jsp link") <br>

