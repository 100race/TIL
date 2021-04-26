# Redirect와 Forward
JSP환경에서 현재 페이지에서 다른페이지로 이동하는 페이지 전환 방식

## Redirect
웹브라우저에게 다른페이지로 이동하라고 명령하여, 다른 WebContainer에 있는 주소로 이동한다.
- 요청정보가 유지되지 않는다.
- URL이 변화하며, 객체를 새로 만든다.
- 사용자가 실수로 글쓰기 중 새로고침을 누르거나 해도 처음 요청한 객체는 저장되어있지않으므로 게시글이 중복되어 작성되거나 하지 않는다.
- 시스템(DB)에 변화가 생기는 요청일 때 적합하다
- ex. 글쓰기기능,로그인,회원가입
- 다른 web container에 있는 주소로 이동가능하다.
- 새로운 페이지에서는 request, response객체가 새롭게 생성된다.
### Redirect 동작
![redirect](https://user-images.githubusercontent.com/46726709/116089932-4d9cbc00-a6de-11eb-99b4-b03d7cf0fe1d.PNG)


## Forward
WebContainer 차원에서 페이지의 이동만 존재한다.
- url이 유지되기때문에 웹브라우저는 다른 페이지로 이동했는지 알 수 없다
- 요청정보가 유지된다
- URL이 유지되며, 객체를 재사용한다
- 웹브라우저에는 최초에 호출한 url만 표시되며 이동한페이지의 url은 확인할 수 없다. (URL유지)
- 현재 실행중인 페이지와 forward에 호출될 페이지는 request,response 객체를 공유한다. (객체재사용)
- 요청정보를 담고있는 url이 페이지가 변한 후에도 유지되기 때문에 요청정보가 여러번 전달되어 동일한 게시글이 여러번 등록될 수 있다. 때문에 시스템에 변화가 생기는 요청에는 적합하지 않다.
- ex. 단순조회, 리스트검색, 리스트보기

 
### Foreward 동작
![forward](https://user-images.githubusercontent.com/46726709/116089930-4c6b8f00-a6de-11eb-8deb-38bfb3fc19d2.PNG)

### 참조
[Redirect VS Forward](https://doublesprogramming.tistory.com/63)<br>
[Forward와 Redirect 차이](https://mangkyu.tistory.com/51)<br>
