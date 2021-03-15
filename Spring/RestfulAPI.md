# Restful 서비스(API)
## REST(Representational State Transfer)란?
  - HTTP URL를 통한 자원의 명시
  - HTTP Method를 통해 해당 자원을 제어하는 행위를 표현
  - 데이터를 주고 받는 형식의 아키텍쳐(디자인 패턴)
  - 하나의 URI는 하나의 고유한 리소스를 대표하도록 설계된다는 개념에 전송방식을 결합해서 원하는 작업을 지정한다. 
  - REST는 HTTP URI로 리소스를 정의하고 HTTP메소드로 리소스에 대한 행위를 정의한다.

## Restful 서비스(API)란?
  - Restful 서비스에서는 그냥 데이터만 처리하고 끝내거나 되돌려줄 데이터를 JSON이나 XML 형식으로 전달. View에 대해서는 전혀 신경쓰지 않는다.
  - 일반적인 서비스의 경우 요청받은 내용을 처리하고 데이터를 가공해서 처리 결과를 특정 플랫폼에 적합한 형태의 View로 만들어 되돌려줌.
  - REST 아키텍쳐를 준수하는 서비스. 데이터를 요청하는 방식이 고정되어 있고, 요청에 따라 데이터를 처리하고 전달하는 작업만 수행
  - 서버는 플랫폼에서 어떻게 사용할지 신경 쓰지 않고, 클라이언트는 받은 데이터를 알아서 가공해서 사용. 멀티 플랫폼에서 사용이 가능하다.
  - 이러한 특성으로 사용자 플랫폼과 View에 상관하지 않고 데이터만 응답해주는 오픈API에서 많이 사용
  - rest 스러운 서비스 라 해서 rest ful.
## RestController
  - 기존 Controller와 ResponseBody를 합친 모습
  - 기존 Controller가 JSP 경로를 리턴했다면 RestController은 순수한 데이터를 반환한다
  - 일반 문자열, JSON, XML등 다양한 포맷의 데이터를 전송한다.
  - RestController에서 사용 가능한 요청 annotation
  - @RequestMapping, @GetMapping, @PostMapping, @PutMapping, @DeleteMapping



### 참조
[스프링 Restful 서비스(API) 개념](https://codevang.tistory.com/260?category=849481)<br>
[스프링부트로 배우는 자바 웹개발 - 윤석진 지음]<br>
