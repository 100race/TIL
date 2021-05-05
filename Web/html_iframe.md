# iframe태그

## iframe이란?
inline frame의 줄임말로 html 웹 문서 안에 또 다른 웹 문서, 또는 동영상 등을 넣을 수 있다. 인라인 요소이며 내용 안에 동영상이나 지도 삽입
가능하다. 요즘은 HTML5가 차세대 웹 표준이 되면서 이를 대체할 <video>,<audio>태그 등이 있으나 이전의 브라우저들(레거시), HTML5표준을 지원하지 않는 브라우저는
 iframe 사용중.


## 속성
사용법 
```html
<iframe src="URL">대체할 내용</iframe>
```
iframe을 지원하지 않는 브라우저일 경우 대체내용을 보여준다
- src : iframe에 삽입될 문서 주소
- width : iframe 너비(px,% 사용)
- height : iframe 높이(px,& 사용)
- frameborder : 테두리를 표시할지 결정(1:테두리존재 0:테두리없음)
- scrolling : 스크롤바 유무(yes:표시 no:없음 auto:자동)
- margintheight: 내용의 top,bottom margin
- marginwidth : 내용의 left, right margin
- align : 정렬방식(top, middle, bottom, left, right)
- name : 타겟이 필요한 프레임의 이름
html5에서 지원하지 않는 속성 : align, frameborder, scrolling, longdesc, marginheight, marginwidth

## 특징
- [html4.0] DOCTYPE에서 Transitional, Frameset에서는 iframe 작동, Strict 문서에서는 작동 x. 
- XSS(cross site scripting)등의 보안이슈들을 야기할 수 있음. 이를 차단하기 위해 서비스 공급자에서 http 헤더를 통해 페이지 렌더링 여부 제한 가능<br>
서비스 공급자는 해당 사이트가 iframe에 표시되는것을 막기위해 header 설정을 통해서 페이지 도메인과 frame의 도메인이 같은지 여부를 확인, 다르면 에러 리턴
- 

### 정리
많이 사용되고있지는 않으며 레거시에서 발견될수있는듯 하다. XSS(cross site scripting)에 취약해 그다지 권장되지는 않음

### 참조
[iframe태그사용법](https://aboooks.tistory.com/205)<br>
[iframe태그란?](https://yeoulcoding.tistory.com/143)<br>
