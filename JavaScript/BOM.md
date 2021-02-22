# BOM

  ![bom](https://user-images.githubusercontent.com/46726709/108722693-c8264f80-7566-11eb-82d1-77e1d066e8fa.png)

  ## BOM(Bowser Object Model ) 이란? 
   브라우저 객체 모델. 웹브라우저의 창이나 브라우저를 제어할 수 있도록 추상화한 것. 전역객체 window의 프로퍼티와 메소드로 제어 가능
   - 객체 모델 종류 : window(최상위), screen, location, navigator, history, document
   - 정확히는 자바스크립트가 아닌 웹브라우저가 제공하는 기능
   - DOM으로 통합해서 칭하기도 한다.
    
   ### Window 객체
   모든 객체가 소속된 객체로 전역객체이며 창이나 프레임을 의미한다.
   - 모든 객체는 window의 자식이다
   - 전역변수와 함수는 window 객체의 프로퍼티와 메소드다
   
   
   ### 예시
   window식별자로 window 객체를 얻을 수 있다. 생략 가능. window객체의 메소드 alert를 호출하는 예시
   ```
   alert('Hello world');
   window.alert('Hello world');
   ```
   
   전역변수 a에 접근하는 예시
   ```
   var a = 1;
   alert(a);
   alert(window.a);
   ```
   
   객체를 만든다 = window 객체의 프로퍼티를 만들다
   ```
   var a = {id:1};
   alert(a.id);
   alert(window.a.id);
   ```
   
   ### Navigator 객체
   브라우저의 정보 제공 객체, 호환성 문제를 위해 사용
   주요 프로퍼티 
   - appName : 웹 브라우저 이름 (ex. ie, nescape)
   - appVersion : 브라우저 버전
   - userAgent : 브라우저가 서버로 전송하는 USER_AGNET HTTP 헤더의 내용
   - platform : 브라우저가 동작하는 운영체제의 정보
   
   ### Location 객체
   윈도우 문서의 주소에 대한 객체. URL 과 관련된 작업을 한다.
    
    
    
    
    
    
    
    
    
   
   
   
   
  ### 참조
  [BOM](https://opentutorials.org/module/904/6633)<br>
  [브라우저 객체 모델 BOM](https://wickies.tistory.com/26)<br>
  [location객체](https://iamawebdeveloper.tistory.com/41)<br>
  
