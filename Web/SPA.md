# Single Page Application(싱글 페이지 어플리케이션)
 ## SPA란?
 단일 페이지 웹 어플리케이션. 화면 이동시에 필요한 데이터를 서버사이드에서 HTML로 전달받지 않고(서버사이드 렌더링 x)
 필요한 데이터만 서버로부터 JSON으로 전달받아 동적으로 렌더링한다.
 - 화면 구성에 필요한 모든 HTML을 클라이언트가 가지고 있으면서, 서버사이드에는 필요한 데이터만 요청해 받기 때문에 기존 어플리케이션에 비해 
 화면 구성 속도가 빠르다.
 - 기존의 서버사이드 렌더링보다 배포가 간단하며, 네이티브 앱과 유사한 사용자 경험을 제공한다.
 - 모바일 사용이 증가하는 현 시점에 SPA의 핵심 가치는 사용자 경험(UX)향상에 있으며 모바일 퍼스트(Mobile First)전략에 부합하다.

 ![spa사진](https://user-images.githubusercontent.com/46726709/109324733-6c2a3680-7898-11eb-8666-da926bf7dc9d.PNG)
 출처 : [what-is-a-single-page-application]https://www.excellentwebworld.com/what-is-a-single-page-application/<br>
 
 ### 장점
 - 트래픽 감소, 속도, 사용성, 반응성의 향상
 
 ### 단점
 - 초기 구동 속도<br>
 SPA는 모든 정적 리소스를 최초에 한번 다운로드 하기 떄문에 초기구동 속도가 상대적으로 느리다. 
 - 검색엔진 최적화(SEO) 문제
 SPA는 서버 렌더링 방식이 아닌 자바스크립트 기반 비동기 모델(클라이언트 렌더링)이다. Angular나 React 등의 SPA 프레임워크는 서버렌더링을
 지원하는 SEO 대응 기술이 이미 존재.
 

#### SEO(검색엔진최적화)
 [SPA와 SSR의 장단점](https://medium.com/aha-official/%EC%95%84%ED%95%98-%ED%94%84%EB%A1%A0%ED%8A%B8-%EA%B0%9C%EB%B0%9C%EA%B8%B0-1-spa%EC%99%80-ssr%EC%9D%98-%EC%9E%A5%EB%8B%A8%EC%A0%90-%EA%B7%B8%EB%A6%AC%EA%B3%A0-nuxt-js-cafdc3ac2053)<br?
 
 
 ### 참고
 [SPA란?](https://velog.io/@josworks27/SPA-%EA%B0%9C%EB%85%90)<br>
 
 
