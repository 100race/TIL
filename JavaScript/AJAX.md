# AJAX

## AJAX(Asynchronous Javascript And XML)란?
- 비동기식 자바스크립트와 xml. 자바스크립트의 라이브러리
- 자바스크립트를 이용해서 비동기적으로 서버와 브라우저가 데이터를 교환할 수 있는 통신 방식을 의미한다.
- 전체 페이지를 새로고침 하지 않고도 일부 부분만 변경되게 하는 기법
- AJAX는 JSON(JavaScript Object Notion)을 사용하는 것이 일반적이다.<br><br>

### 동기식 처리 모델 VS 비동기식 처리 모델
- 동기식 : 직렬적. 서버에 데이터를 요청한 이후 데이터가 올때까지 대기하며 이후 작업 중단.(Blocking)
- 비동기식 : 병렬적. 서버에 데이터를 요청한 이후 데이터를 기다리지 않고(Non-Blocking) 즉시 다음 작업 수행. 자바스크립트 대부분의 DOM 이벤트와 Timer함수 (setTimeout, setInterval), Ajax요청은 비동기적으로 동작.

### 장점 : 자원 낭비를 줄일 수 있고 빠르다<br>
 사용자가 먼저 폼을 보낸 페이지와 반응으로 오는 페이지는 비슷한 경우가 많다. 페이지 전체를 새로고침하면 대역폭 낭비가 심하므로 일부분만 바꿔
 방비를 줄이는 기법.
- 페이지 이동없이 화면 전환이 빠르고 부드럽다.
- 웹 서버에서 전적으로 처리되던 데이터 처리의 일부분이 클라이언트 쪽에서 처리 되므로 웹 브라우저와 <br>
 웹 서버 사이에 교환되는 데이터량과 웹서버의 데이터 처리량도 줄어들기 때문에 애플리케이션의 응답성이 좋아진다 <br>
- 서버 처리를 기다리지 않고, 비동기 요청이 가능하다.
- 수신하는 데이터 양을 줄일 수 있고, 클라이언트에게 처리를 위임할 수도 있다.
- 플러그인 없이도 인터렉티브한 웹페이지 구현할 수 있다.
 
### 단점  <br> 
- Ajax를 쓸 수 없는 브라우저에 대한 문제가 있다.
- HTTP 클라이언트의 기능이 한정되어 있다.
- 페이지 이동없는 통신으로 인한 보안상의 문제
- 지원하는 Charset이 한정되어 있다.
- 스크립트로 작성되므로 디버깅이 용이하지 않다.
- 요청을 남발하면 역으로 서버 부하가 늘 수 있음.
- 동일-출처 정책으로 인해 다른 도메인과는 통신이 불가능하다.

## 예제
 GET을 사용하여 Ajax 요청을 하는 단순 예제이다.


get-ajax-data.js:
```
// 클라이언트-사이드 스크립트

// Ajax 요청을 초기화합니다
var xhr = new XMLHttpRequest();
xhr.open('get', 'send-ajax-data.php');

// 요청의 상태 변화를 추적합니다
xhr.onreadystatechange = function(){
	if(xhr.readyState !== 4) return;
	// readyState 4: 완료

	if(xhr.status === 200) {
    // status 200: 성공
		console.log(xhr.responseText); // '반환된 텍스트'
	} else {
		console.log('에러: ' + xhr.status); // 요청 도중 에러 발생
	}
}
```
send-ajax-data.php:
```
<?php
// 서버-사이드 스크립트

// 내용의 형식을 설정합니다
header('Content-Type: text/plain');

// 데이터를 보냅니다
echo "반환된 텍스트";
?>
jQuery 예제
jQuery에서는 $.ajax를 사용하거나 요청 방식에 따라 $.get 또는 $.post 를 사용한다.

$.get('send-ajax-data.php').done(function(data) {
    console.log(data); //  '반환된 텍스트'
}).fail(function(data) {
    console.log('에러: ' + data); // 요청 도중 에러 발생
});
```

### 참조
[AJAX](https://ko.wikipedia.org/wiki/Ajax, "Ajax link") <br>
[AJAX란 무엇인가?](https://velog.io/@surim014/AJAX%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80, "Ajax link") <br>
[jQuery Ajax & JSON | PoiemaWeb](https://poiemaweb.com/jquery-ajax-json)<br?
