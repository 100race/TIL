# var,let,const
  
  var은 function-scoped 고 let,const는 block-scoped이다. <br>
  var은 변수 재선언 가능하지만 let,const는 변수 재선언 가능하다. <br>
  let과 const의 차이점은 let은 변수에 재할당이 가능하지만 const는 재할당이 불가능하다는 것이다. <br>
  
 ## var (변수 재선언 가능)
 ```javascript
 var vartest = '변수재선언가능';
 var vartest = '다시재선언가능';
 ```
 필요한때 자유롭게 맘대로 선언할 수 있지만, 같은이름에 다시 할당이 될수있어 프로그래밍할 때 혼돈을 야기할 수 있다.
 
 ## let (변수 재선언 불가능, 변수 재할당 가능)
 ```javascript
 let vartest = '변수재선언가능';
 ~~~let vartest = '다시재선언불가능';~~~
 vartest = '변수재할당가능';
 ```
 ## const (변수 재선언 불가능, 변수 재할당 불가능) 
 ```javascript
 const vartest = '변수재선언가능';
 ~~~const vartest = '다시재선언불가능';~~~
 ~~~consttest = '변수재할당불가능';~~~
 ```
 
 
 ### 정리
 vue.js 개발하다보니 var, let, const의 사용이 많아 차이점을 명확히 하고자 간단히 정리했다.
 변수 재할당이 필요할 경우 let을 사용하고 재할당이 필요없을 경우 const를 사용하면 좋다.
 
 
 
 
 
 ### 참조
 [ver,let,const 차이점](https://gist.github.com/LeoHeo/7c2a2a6dbcf80becaaa1e61e90091e5d)<br>
 [ver,let,const 비교](https://backstreet-programmer.tistory.com/76)<br>
