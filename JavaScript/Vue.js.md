# Vue.js
  ## Vue.js란?
  웹 화면을 만들기 위한 프론트엔드 프레임워크. Angular,React 등이 있다. Vue layer에 집중된 경량 UI라이브러리. 
  
  ### 
  
  ### 선언적 렌더링
  app.vue 파일, 
  - 화면 구조
  main.js 파일 구조
  - 라우터 정의,
  - 렌더링 할 마운트
  예제
  ```
  <div id="app">
  {{ message }}
</div>
  ```
  
  ```
  var app = new Vue({
  el: '#app',
  data: {
    message: '안녕하세요 Vue!'
  }
})
```

  ## Vue파일 구조
  한 컴포넌트에서 HTML,Script,CSS를 관리하는데 이것을 싱글 파일 컴포넌트라고 한다.
  ```
  <!--HTML을 작성하는 부분-->
  <template></template>
  <!-- script을 정의하는 부분-->
  <script></script>
  <!--css를 정의하는 부분-->
  <style></style>
  ```
  
  ## Vue.js VS React
  |Vue.js|React|
  |-----|-----|
  |템플릿형식 제작|??|
  |간단함|대규모 개발|
  |빠르고 경량|??|
  
  
  
  
  spa
  

  
  
  
  
  
  
  
  ### 참고
  [Vue.js 시작하기 - vuejs.org](https://kr.vuejs.org/v2/guide/index.html)<br>
  [React 인가 Vue 인가?](https://joshua1988.github.io/web_dev/vue-or-react/)<br>
