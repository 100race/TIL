# Session(세션)

## 세션트래킹이란?
  HTTP 프로토콜은 비연결 지향이기 때문에 이전 웹페이지에서의 작업을 기억 못한다. 각 페이지나 서블릿의 상태, 정보를 다른 페이지와 연결해 주는 것.
  세션과 쿠키를 이용한다.
  
  ### 세션과 쿠키의 차이
  
  |구분|세션|쿠키|
  |---|---|---|
  |저장위치|서버|클라이언트|
  |저장 데이터 타입|객체|텍스트(문자열)|
  |저장 데이터 크기|서버에서 수용 가능한 만큼|제한 있음|
  |보안|좋음|안좋음|
  
 ## Session(세션)이란?
  연결 지속성을 제공하기 위해 서버에 저장되는 정보. 서버에 정보를 요청할 때 생성되는 상태정보
  - 클라이언트의 개수만큼 만들어진다 ( 클라이언트들의 정보가 섞이면 안되기 때문)
  - 디폴트 지속시간은 30분. 시간은 임의로 가능
  ### 세션ID
   - 쿠키 기술로 클라이언트에 저장된다
  ### 세션 바인딩
   - WAS의 컨테이너가 관리하는 세션을 서블릿에서 사용할 수 있도록 제공하는 작업
  ### 세션 트래킹
   - 클라이언트에서 전달된 세션아디이와 동일한 세션을 찾는 직업
  ### 세션과 관련된 메소드
    - HttpSession : 
      클라이언트의 정보를 세션명(String)과 세션값(Object)의 형태로 저장하기 위한 인스턴스
      
    - HttpServletRequest.getSession() : 
      세션을 바인딩 해서 반환하는 메소드. 
      세션id가 없거나 탐색 실패 -> 새로 생성해서 바인딩 하고 반환.
      클라이언트 세션아이디에 해당되는 세션이 탐색 됨 -> 세션 트래킹해서 바인딩 하고 반환
      세션이 바인딩 되어야만 서블릿에서 사용
      세션이 생성되어 바인딩 된 경우, 세션ID를 클라이언트에 쿠키로(JSESSIONID) 전달해 저장
      
    - HttpServletRequest.getSession(boolean create) : 
      세션을 바인딩 하여 반환하는 메소드
      false 전달 -> 세션 생성하지 않고 탐색하여 바인딩
      true 전달 -> 세션 생성 및 탐색하여 바인딩
      
    - session.isNew() : 
      세션을 새로 생성해서 바인딩 한 경우 true 반환. 트래킹 해서 반환할 경우 false 반환
      
    - session.getId() : 
      세션 아이디를 반환하는 메소드 (클라이언트에 저장된 JSESSIONID와 동일)
      
    - session.getCreationTime() : 
      세션 생성시간을 반환
      
    - session.getMaxInactiveInterval() : 
      세션 지속시간을 반환 (초)
      
    - session.setMaxInactiveInterval(초) : 
      세션 지속시간을 변경 (디폴트 30분)
      
    - HttpSession.setAttribute(String attributeName, Object attributeValue)
      세션속성명(String) 과 속성값(Object)를 한쌍으로 세션에 정보를 저장
      속성명이 중복일 경우 덮어쓰기. 쿠키와 유사하지만 value가 객체인 점이 다르다
      
    - HttpSession.getAttribute(String attributeName) : 
      세션 속성명으로 속성값을 반환
      세션속성값을 Object 인스턴스로 반환하므로 객체형변환하여 사용
      세션속셩명이 없는 경우 null 반환 (ex . 로그인 안 된 상태)
 
 
 
 
 
 ### 참조
 [Session](https://codingwanee.tistory.com/entry/%EC%9B%B9%EA%B0%9C%EB%B0%9C-%EC%84%B8%EC%85%98) <br>
 [세션트래킹](https://stothey0804.github.io/java/session-tracking/)
