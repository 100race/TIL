# Restful 서비스(API)
## REST(Representational State Transfer)란?
  - HTTP URL를 통한 자원의 명시, HTTP Method를 통해 해당 자원을 제어하는 행위를 표현<br>
  URI를 통해 자원을 명시한다는 말은 "URL?name="oo"방식의 쿼리스트링 또는 @PathVariable 어노테이션을 통해 "URL/oo" 방식으로 URI에 필요한
  데이터를 넣어 전송하는 것을 의미한다. REST 방식에서는 두번째 방식을 사용
  - REST는 HTTP URI로 리소스를 정의하고 HTTP메소드로 리소스에 대한 행위를 정의한다.
  - 데이터를 주고 받는 형식의 아키텍쳐(디자인 패턴)
  - 하나의 URI는 하나의 고유한 리소스를 대표하도록 설계된다는 개념에 전송방식을 결합해서 원하는 작업을 지정한다. 

## Restful 서비스(API)란?
  - Restful 서비스에서는 그냥 데이터만 처리하고 끝내거나 되돌려줄 데이터를 JSON이나 XML 형식으로 전달. View에 대해서는 전혀 신경쓰지 않는다.
  - 일반적인 서비스의 : 요청받은 내용을 처리하고 데이터를 가공해서 처리 결과를 특정 플랫폼에 적합한 형태의 View로 만들어 되돌려줌.
  - Restful 서비스 : 데이터를 요청하는 방식이 고정되어 있고, 요청에 따라 데이터를 처리하고 전달하는 작업만 수행
  - 서버는 플랫폼에서 어떻게 사용할지 신경 쓰지 않고, 클라이언트는 받은 데이터를 알아서 가공해서 사용. 멀티 플랫폼에서 사용이 가능하다.
  - 이러한 특성으로 사용자 플랫폼과 View에 상관하지 않고 데이터만 응답해주는 오픈API에서 많이 사용
  - Rest 스러운 서비스라 해서 Rest + ful.
## RestController
  - 기존 Controller와 ResponseBody를 합친 모습
  - 기존 Controller가 JSP 경로를 리턴했다면 RestController은 순수한 데이터를 반환한다
  - 일반 문자열, JSON, XML등 다양한 포맷의 데이터를 전송한다.
  - RestController에서 사용 가능한 요청 annotation : @RequestMapping, @GetMapping, @PostMapping, @PutMapping, @DeleteMapping
  
## 클라이언트 -> 서버 요청규칙
- URL/oo 방식으로 URL에 필요한 데이터를 넣어 전송.
- URI 규칙 
  1. 하이픈(-)은 가능하지만 언더바(_)는 x
  2. 특별한 경우를 제외하고 대문자는 사용하지 않는다
  3. URI 마지막에 / 사용하지않는다
  4. 확장자가 포함된 파일 이름을 직접 포함시키지 않는다.
- 기존 서비스는 GET,POST 타입만 사용. 어떤 작업 처리 요청인지는 URL 매핑을 통해 들어온 데이터를 적절히 처리
- Restful에서는 HTTP Method의 타입으로 어떤 작업을 할지 판별. PUT과 DELETE 타입을 추가
- 
 |게시판 예시| 기존 서비스에서의 요청 | Restful서비스에서의 요청|
  |-------|--------|-----------|
  |글읽기|[GET]URL/read?no=123|[GET]URL/123|
  |글쓰기|[POST|URL/write|[POST]URL|
  |글삭제|[GET]URL/delete?no=123|[DELETE]URL/123|
  |글수정|[POST]/update|[PUT]URL/123|
  
  |HTTP Method 타입| CRUD |
  |-------|--------|
  |POST|[create(insert)|
  |GET|read(select)|
  |DELETE|delete|
  |PUT|update|
  
## 서버 -> 클라이언트 응답코드
- 데이터는 JSON이나 XML 형태로 보내주며, 처리 결과는 상태코드로 보내준다. HTTP의 상태 코드를 그대로 사용
### HTTP 상태코드
|상태코드| 설명 |
  |-------|--------|
  |200번대| 클라이언트가 요청한 작업을 서버가 성공적으로 수행했다|
  |200| OK 요청에 대한 작업을 정상적으로 완료|
  |201| Created POST 요청을 정상적으로 완료(create,insert) ex.회원가입|
  |204| No Content 요청이 정상적으로 수행되고 이 요청과 관련되었던 컨텐츠 또한 더 이상 존재하지 않음. ex.게시글 삭제|
  
  |300번대| 리다이렉션에 관련된 상태|
  |301| Moved Permanently 요청한 리소스에 대한 URI가 변경되었을 때, 새로운 URI와 함께 회신|
  |304| Not Modified 요청한 리소스가 이전 요청때와 달라진 점이 없을 때. 수정되지 않음|
  
  |400번대| 클라이언트의 요청이 잘못된 경우 / 프론트 엔드 |
  |400| Bad Request 부적절한 요청|
  |401| Unauthorized 인증되지 않은 사용자. 비로그인 호출 등에 사용|
  |403| Forbidden 접근이 금지된 리소스를 요청|
  |404| Not Found 요청한 리소스를 찾을 수 없음|
  |405| Method Not Allowed 요청 리소스를 처리하는데 부적합한 Method|
  |406| No Acceptable 서버 주도 컨텐츠 협상을 했음에도 알맞은 컨텐츠 타입이 없음|
  |408| Request Timeout 클라이언트와 서버의 연결은 되었지만 요청의 본문이 서버에 도착하지 않는경우|
  |429| Too Many Requests 너무 많은 서버요청|
    
  * 서버주도 컨텐츠 협상 : 클라이언트가 서버에 리소스 요청할 때 HTTP 헤더의 Accept 필드를 사용해 어떤 컨텐츠 타입의 리소스를 원하는지 함께 전달. text/html 등등. 요청받은 서버는 Accept 필드를 보고 요청받은 리소스와 맞는 컨텐츠 타입이 있는지 살펴보고 알맞은 리소스를 찾는다.

  |500번대| 서버에서 잘못 된 경우 / 백엔드|
  |500| Internal Server Error 서버의 뭔가 알 수 없는 에러 핸들링되지 않은 에러|
  |502| Bad Gateway 백엔드 어플리케이션이 죽은 상황|
  |503| Service Unavailable 서버가 요청을 처리할 준비가 되지 않았음|
  |504| Gateway Timeout 요청에 대한 타임아웃. 408과 다르게 백엔드 아키텍쳐 내부 서버에서 발생한 타임아웃|



## 서버 -> 클라이언트 응답데이터
- JSON


### 참조
[스프링 Restful 서비스(API) 개념](htps://codevang.tistory.com/260?category=849481)<br>
[스프링부트로 배우는 자바 웹개발 - 윤석진 지음]<br>
[서버의 상태를 알려주는 HTTP 상태코드](https://evan-moon.github.io/2020/03/15/about-http-status-code/)<br>
