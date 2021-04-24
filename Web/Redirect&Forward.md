# Redirect와 Forward
JSP환경에서 현재 페이지에서 다른페이지로 이동하는 페이지 전환 방식
## Redirect
- 요청정보가 유지되지 않는다.
- URL이 변화하며, 객체를 새로 만든다.
- 시스템(DB)에 변화가 생기는 요청
- ex. 글쓰기기능,로그인,회원가입
- 다른 web container에 있는 주소로 이동가능하다.
- 새로운 페이지에서는 request, response객체가 새롭게 생성된다.
### Redirect 동작


## Forward
- 요청정보가 유지된다
- URL이 변화하지 않으며 객체를 재사용한다.
- ex. 리스트검색, 리스트보기
- 현재 실행중인 페이지와 forward에 호출될 페이지는 request,response 객체를 공유한다.
 
### Foreward 동작


### 참조
[Redirect VS Forward](https://doublesprogramming.tistory.com/63)<br>
