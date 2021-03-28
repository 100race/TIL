# Vue.js
  ## Vue.js란?
  웹 화면을 만들기 위한 프론트엔드 프레임워크. Angular,React 등이 있다. Vue layer에 집중된 경량 UI라이브러리. 
  
  ## Vue.js의 특징
  1. 가상돔(Virtual DOM)으로 화면 요소를 변경 및 조작하고 최종결과물을 DOM tree에 반영
  2. 컴포넌트 기반 개발 방식 : 화면을 여러개 작은 단위로 쪼개어 개발. 재사용성, 구현속도, 코드 가독성 증가
  3. MVVM 패턴 : 화면 UI  코드와 백엔드 데이터 처리 코드를 분리
  ![mvvm](https://user-images.githubusercontent.com/46726709/112732481-8af61880-8f7d-11eb-9cbd-458ce8587845.PNG)
  4. 기존 프레임워크의 장점 흡수 : 리액트, 앵귤러의 장점인 two-way 데이터바인딩과 Virtual DOM 기능 채용
  5. 반응형 웹 : 데이터와 DOM을 연결

  ### 선언적 렌더링
  vue.js의 핵심은 간단한 템플릿을 사용해 선언적으로 DOM에 데이터를 렌더링 하는 것.
  - app.vue 파일<br> 
    - [싱글파일컴포넌트](https://github.com/100race/TIL/blob/main/JavaScript/Vue.js.md#%EC%8B%B1%EA%B8%80-%ED%8C%8C%EC%9D%BC-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-sfc)
    - 화면 구조<br>
  - main.js 파일 구조 <br>
    - 라우터 정의 <br>
    - 렌더링 할 마운트 <br>
  - simple 예제
  ```
    >>html부분
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
	// Vue를 사용하기 위하여 CDN 정의
<div id="app">
  <p>{{ title }}</p>
   //  {{ Mustache(interpolation) }}
        vue에서 선언된 속성내의 변수나 함수를 호출
        js부분에에 있는 data.title 값인 안녕 VueJS!를 출력
</div>

  ```
  
  ```
  >>자바스크립트부분
  new Vue({   // Vue를 선언한다
  el: ‘#app’, // Vue가 정의될 때 해당 Vue가 적용될 요소를 지정    여기서는 HTML 코드에 선언된 id="app"인 div 태그를 지정
  data: { // data 는 해당 VueJS에서 사용할 정보들을 선언해주는 역할
    title: '안녕 VueJS!‘  // title이라는 변수를 만들어 안녕 VueJS란 값을 넣어줌. 이 부분은 HTML의  Mustache 부분이 호출
  }   
})

  ```
   ## Vue.js 구성요소
 ##### 뷰를 레고블럭에 비유
 - 조립판 : 뷰 인스턴스
 - 레고블럭을 각 위치에 설치 : 뷰 컴포넌트를 라우팅으로 연결
 - 레고블럭들 : 뷰 컴포넌트 설계 및 생성
 - 설치한 레고블럭 꾸미기 : 뷰 컴포넌트 내용(뷰 템플릿) 구현
 ##### 구성요소
 - Vue instance : 뷰로 개발할 때 필수로 생성해야 하는 단위
  ```
  new Vue({
    el: //인스턴스가 뿌려질 지점
    template: //인스턴스의 화면 내용
    data: //인스턴스가 갖는 데이터
    methods: //인스턴스의 이벤트 정의
    created: //인스턴스 라이프 사이클
  ```
 - Vue component : 화면을 구조적으로 설계하기 위한 요소
 ```
 Vue.component('my-app',{
  //인스턴스 옵션 속성과 동일
  template: //인스턴스의 화면 내용 
  data: //인스턴스가 갖는 데이터
  methods: //인스턴스의 이벤트 정의
  created: //인스턴스 라이프 사이클
 ```
 - Vue router : 여러개의 화면 간에 이동방법
 ```
 var Main = { template : '<div>main</div>' };
 var Login = { template : '<div>login</div>' };
 
 var router = new VueRouter({
  routes:[
    {path: '/main', component: Main},
    {path: '/login', component: Login}
    ]
  });
  
  var app = new Vue({
  el : '#app',
  router: router
  });
 ```
 - Vue template : 화면을 구체적으로 꾸미는 방법 및 문법
 ```
 {{message}},
 {{message.splite('').reverse().join('') }}
 <p v-bind:id = "uid">인스턴스의 값과 연결</p>
 <button v-on:click="pAlert">클릭하면 경고창 표시</button>
 <ul v-for="item in items">{{item.name}}</ul>
 <a v-if="seen">seen 값에 따라 표시 여부 결정</a>
 ```

 
  ## .vue파일 구조
  기존의 페이지 내 Vue 선언 방식의 단점
  - Global definitions - 모든 컴포넌트가 고유한 이름 필요
  - String templates - 구문 강조가 약하다. HTML 에 보기 안좋은 슬래시
  - No CSS support - CSS를 지원안하는게 아니라, CSS가 눈에 띄게 모듈화 되지 않음
  - No build step - 전처리기가 아닌 HTML 및 ES5 JavaScript로 제한
  이런 약점을 해결한 SFC
  
  ### 싱글 파일 컴포넌트 (SFC)
  싱글 파일 컴포넌트는 화면의 특정 영역에 대한 HTML,scipt,CSS 코드를 한 파일에서 관리하는 방법.
  뷰 CLI 프로젝트를 생성하고 나면 App.vue라는 파일을 확인할 수 있다. 이처럼 vue 확장자를 가진
  파일을 모두 싱글 파일 컴포넌트라 한다.
  ```
  <!--HTML을 작성하는 부분-->
  <template></template>
  <!-- 자바스크립트 (뷰 컴포넌트 내용, 데이터) 부분-->
  <script></script>
  <!--css를 정의하는 부분 (뷰 템플릿의 스타일)-->
  <style></style>
  ```
  - 싱글 파일 컴포넌트는 뷰 로더에 의해 HTML,CSS,JS와 같은 웹 자원으로 분리되어 실행. 뷰 로더는 웹팩의 로더 종류 중 하나이고 뷰 CLI로 프로젝트를 생성하면 기본적으로 설정되어있다.
  - template : 직접적으로 화면에 표시할 내용의 코드가 들어가는 부분. HTML Tag가 들어가며, vue의 데이터 바인딩이 추가됨
  - script : vue components의 내용이 정의되는 내용. v-dom에 대한 life cycle 개념이 추가된다. 
  - style : template에서 구성한 html에 대한 css 스타일을 정의하는 영역
  
  ## Vue.js VS React
  |Vue.js|React|
  |-----|-----|
  |SFC,템플릿형식 제작|JSX기반 컴포넌트 구문|
  |간단한 syntax와 프로젝트 설정|대규모 개발|
  |빠르고 경량|더 큰 개발 생태계|
  ||web과 native 앱 개발에 모두 사용가능|
  
  ### 공통점
  - virtual DOM 을 사용한 빠른 렌더링
  - Reactive Component  반응형 컴포넌트 기반 개발 <br>
     컴포넌트는 다른 프로젝트에서 재사용 가능하고 캡슐화와 확장이 가능해 개발이 유연해진다.
  - 경량 라이브러리
  - Server Side Rendering 서버사이드 렌더링
  - 라우터, 번들러, state management 와 결합 쉬움
  - 방대한 개발환경과 커뮤니티, 지원

  

  
  

  
  
  
  
  
  
  
  ### 참고
  [Vue.js 시작하기 - vuejs.org](https://kr.vuejs.org/v2/guide/index.html)<br>
  [React 인가 Vue 인가?](https://joshua1988.github.io/web_dev/vue-or-react/)<br>
  [싱글 파일 컴포넌트](https://kr.vuejs.org/v2/guide/single-file-components.html)<br>
  [Vue입문자를 위한 공개세미나](https://www.slideshare.net/GihyoJoshuaJang/do-it-vuejs-88453012?qid=53ef1435-7ebc-4edc-97f5-6999b7f7ef75&v=&b=&from_search=9)<br>
  [맨땅에 Vue.js](https://medium.com/@hozacho/%EB%A7%A8%EB%95%85%EC%97%90-vuejs-8a50055b7551)<br>
