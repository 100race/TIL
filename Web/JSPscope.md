 
 # Scope객체
 
 JSP 페이지 이동시 값을 가져가는게 불편하다. 이를 위해서 활용하는 객체. 
 - 속성(Attribute) : 공유되는 데이터
 - 영역(Scope) : 속성을 공유할 수 있는 유효범위, 생존기간
 - 4개의 영역 범위가 존재 page, request, session, application
 
   ### page 
   현재 페이지
   하나의 JSP 페이지 내에서 지역변수처럼 사용되어 공유될 값을 저장한다.
   해당 페이지가 클라이언트에 서비스를 제공하는 동안에 유효.
   
   ### request
   현재 요청이 끝날 때까지
   http요청을 WAS가 받아서 웹 브라우저에 응답할 때 까지 변수가 유지되는 경우 사용
   클라이언트의 요청이 처리되는 동안 유효
   한번의 요청을 처리하는데 사용되는 모든 JSP 페이지에서 공유될 값을 저장. 하나의 요청을 처리하는데 사용되는 JSP페이지 사이에서
   정보를 전달하기 위해 사용
   
   ### session
   세션이 종료될 때 까지(로그아웃 할때까지)
   웹 브라우저 별로 변수가 관리되는 경우 사용
   한 사용자와 관련된 정보를 JSP들이 공유하기 위해서 사용. ex. 사용자의 로그인 정보
   
   ### application
   웹 어플리케이션 종료시 까지
   웹 어플리케이션이 시작되고 종료될 때까지 변수가 유지되는 경우 사용
   모든 사용자와 관련해서 공유할 정보를 저장. 임시 디렉토리 경로와 같은 웹 어플리케이션의 설정 정보를 주로 저장.
   
  ## scope 객체의 속성 처리 메서드
  - setAttribute(String name, Object value)
  - getAttribute(String name)
  - removeAttribute(String name)
  - getAttributeNames()


### 참조
[영역 객체와 속성](https://blog.naver.com/javaking75/140181686711, "jsp link") <br>
[scope란?](https://m.blog.naver.com/PostView.nhn?blogId=good_ray&logNo=221325440532&proxyReferer=https:%2F%2Fwww.google.com%2F, "jsp link") <br>
[객체 범위](https://victorydntmd.tistory.com/155, "jsp link") <br>

