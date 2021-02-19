# Event bubbling & capturing (이벤트버블링 & 캡쳐링)
표준 DOM 이벤트의 흐름
![이벤트리스너](https://user-images.githubusercontent.com/46726709/108453123-288a6800-72ad-11eb-9aa9-4a55e2f52789.PNG)
  - 캡처링 단계 – 이벤트가 하위 요소로 전파되는 단계
  - 타깃 단계 – 이벤트가 실제 타깃 요소에 전달되는 단계
  - 버블링 단계 – 이벤트가 상위 요소로 전파되는 단계 <br>
 input에서 이벤트가 발생하면 최상위 조상에서 시작해 아래로 내려오고(캡쳐링) 이벤트가 타켓에 도착해 실행된 후(타겟 단계) 다시 위로 올라간다(버블링). 
 

  ## Bubbling(버블링)
  한 요소에 이벤트가 발생하면 그 요소에 할당된 핸들러 + 부모 요소의 핸들러가 동작.
  가장 최상단의 조상 요소를 만날 때까지 이 과정이 반복되면서 요소 각각에 할당된 핸들러가 동작한다.
  이런 흐름을 '이벤트 버블링’이라고 부른다. 이벤트가 제일 깊은 곳에 있는 요소에서 시작해 부모 요소를 거슬러 올라가며 발생하는 모양이 마치 물속 거품(bubble)과 닮았기 때문.
  
  ```
 <style>
  body * {
    margin: 10px;
    border: 1px solid blue;
  }
</style>

<form onclick="alert('form')">FORM
  <div onclick="alert('div')">DIV
    <p onclick="alert('p')">P</p>
  </div>
</form>
  ```
  실행순서 : p 의 onclick 이벤트 핸들러 -> div의 이벤트 핸들러 -> form의 이벤트 핸들러
  
  > 거의 모든 이벤트는 버블링 된다.
  
   ### 버블링 중단
  현재 이벤트를 처리하고 난 뒤 버블링 중단.위로 거슬러 올라가는 event를 중단시킴. 
  ```
  <button onClick = "event.stopPropagation()"></button>
  ```
  - 위로가는 버블링은 막아주지만 이 요소에 적용된 다른 핸들러들의 동작까지 막지는 못함
  - 버블링을 멈추고 다른 핸들러의 동작도 멈추려면 event.stopImmediatePropagation()
  - 진짜 필요할 때만 사용하기. 문제상황 발생 가능 (ex. 사용자의 행동패턴을 분석하는 시스템으로 분석할때 stopPropagation은 분석시스템 코드가 동작하지 않음. '죽은영역'된다.
  
  ## Event.target
  이벤트가 어디서 발생했는지에 대한 정보. 이벤트가 발생한 가장 안쪽의 요소.
  
  ### event.target 과 this의 차이점
    - event.target은 실제로 이벤트가 시작된 요소. 일어난곳. 버블링에 상관없음
    - this는 현재 실행중인 핸들러가 할당된 요소. this(event.currentTarget)
    
  ## Capturing(캡쳐링)
  이벤트가 최상위 조상에서 타겟요소까지 내려오는 것. 이벤트가 실행 될 때 빼고 잘 이용하지 않음.
  on<event> 프로퍼티나 addEventListener(event,hendler)을 이용해 할당된 핸들러는 캡처링과정 동작하지 않는다. 타겟단계와 버블링 단계만 동작하게 된다.
  핸들러가 캡쳐링 단계에서 동작하게 하려면 addEventListener의 capture 옵션을 true로 설정
  ```
  target.addEventListener(x,{capture:true})
  target.addEventListener(x,true)
  ```
  
  
  
  

### 참조
[버블링과 캡처링](https://ko.javascript.info/bubbling-and-capturing)<br>
[W3C - UI Events](https://www.w3.org/TR/DOM-Level-3-Events/)<br>
