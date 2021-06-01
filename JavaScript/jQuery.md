# jQuery란?
모든 웹 브라우저에서 동작하는 클라이언트용 자바스크립트 라이브러리. 언어. 자바스크립트에서 자주 사용하는 기능을 미리 만들어둔 것으로, 자바스크립트 사용을 쉽게 하도록 도와줌.

## 장점
- 가볍다
- 비동기 통신(ajax)할 수 있도록 구현됨
- 동적으로 객체모델을 통해 html이나 css를 조작하는것이 편리 ( html 요소, css 속성 변경 함수 포함)

## jQuery 라이브러리 설정
1. 파일 다운로드 후 외부 자바스크립트 파일로 추가

    http://jquery.com/download 접속, 다운로드 후 추가

2. CDN 호스트 사용
- CDN(Content Delivery NEtwork)란?<br>
파일을 여러 서버에 분산시키고 사용자가 접속하는 지역과 가장 가까운 곳의 서버에서 파일을 전송하는 기술

    https://code.jquery.com/에 접속
```javascript
<script
  src="https://code.jquery.com/jquery-3.6.0.js"
  integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk="
  crossorigin="anonymous"></script>
```
### 참조
HTML웹프로그래밍입문 -윤인성 저 한빛아카데미<br>
[jQuery정의/라이브러리/선택자](https://immimiim.tistory.com/22)<br>
