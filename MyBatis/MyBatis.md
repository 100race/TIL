# MyBatis

## MyBatis란?
  자바의 데이터베이스 프로그래밍을 조금 더 쉽게 도와주는 프레임워크. JDBC를 조금 더 쉽게 다루기 위해 개발됨.
  
  ### MyBatis 특징
  - SQL문이 코드로부터 분리 <br>
  기존 : DAO에 SQL문 작성 -> Mapper 파일에 SQL코드 입력
  - 생산성 : <br>
  코드가 짧아짐
  - 유지보수성 향상 :  <br>
  Mapper파일에만 SQL코드를 입력하므로 이곳에서만 유지보수를 하면 다른곳에 영향이 없다
  
  ### MyBatis 구성

  
  |이름|역할|
|------|---|
|MyBatis 환경설정 파일 (SqlSessionConfig.xml)|데이터베이스의 접속 주소 정보나 Mapping 파일의 경로 등의 고정된 환경정보를 설정한다|
|SqlSessionFactoryBuilder|MyBatis설정 파일을 바탕으로 SqlSessionFactory를 생성한다.|
|SqlSessionFactory|SqlSession을 생성한다|
|SqlSession|핵심적인 역할을 하는 클래스. SQL 실행이나 트랜잭션 관리를 실행. thread-safe하지 않으므로 thread마다 필요시 생성|
|mapping파일 (user.xml) |SQL문과 OR Mapping 설정 |
 
 
 ### 참조
 [MyBatis란 무엇인가?](https://m.blog.naver.com/PostView.nhn?blogId=wwwkang8&logNo=220989381100&proxyReferer=https:%2F%2Fwww.google.com%2F) <br>
 [MyBatis개요](https://www.youtube.com/watch?v=9b5P4YiyqOY&ab_channel=SKplanetTacademy) <br>
