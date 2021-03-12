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
  
  ### MyBatis 구성요소
  
  |이름|역할|
|------|---|
|MyBatis 환경설정 파일 (SqlSessionConfig.xml)|데이터베이스의 접속 주소 정보나 Mapping 파일의 경로 등의 고정된 환경정보를 설정한다|
|SqlSessionFactoryBuilder|MyBatis설정 파일을 바탕으로 SqlSessionFactory를 생성한다.|
|SqlSessionFactory|SqlSession을 생성한다|
|SqlSession|핵심적인 역할을 하는 클래스. SQL 실행이나 트랜잭션 관리를 실행. thread-safe하지 않으므로 thread마다 필요시 생성|
|mapping파일 (user.xml) |SQL문과 OR Mapping 설정 |

(1)매퍼(Mapper)
- 두가지 종류.
- SQL을 XML에 정의된 XML로 생성
- SQL을 메소드에 어노테이션으로 정의한 인터페이스로 생성
- mapper파일 선언

```
<!DOCTYPE mapper
PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="bbs"> 
                 :
</mapper>
  ```
  - Mapper구조는 DTD선언 밑에 <mapper>루트 엘리먼트가 선언.
  - mapper 엘리먼트는 namespace속성을 가진다

   1-1. select
   ```
   <select id=”selectPerson” parameterType=”int” resultType=”hashmap”>
      SELECT * FROM PERSON WHERE ID = #{id}
    </select>
   ```
   - id 속성 : 필수속성으로 전체 Mapper파일들 내에서 유일한 아이디 등록
     - Mapper루트태그(<Mapper namespace="">)의 namespace가 다르면 같은 id도 다른 id로 인식된다.
   - parameterType 속성 : 외부로부터 데이터를 받아올 때 사용. insert, update시 사용할 데이터를 받아와서 생성,수정
   - resultType 속성 : 주로 select 구문 처리 후 DBMS로부터 결과를 받아올 때 사용. 결과값을 매핑할 자바 객체 타입을 명시한다. select 구문에서 필수
   1-2. insert, update, delete 
    - insert의 selectKey는 기본 키 필드의 자동생성을 지원
    - <selectKey>를 사용하면 생성된 키를 쉽게 가져올 수 있다.
```
  <insert id="insertAuthor" parameterType="domain.blog.Author">
        <selectKey keyProperty="id" resultType="int" >
                select board_seq.nextval as idfrom dual
        </selectKey>
        insert into Author (id,username,password,email,bio)
        values (#{id},#{username},#{password},#{email},#{bio})
</insert>
 
<update id="updateAuthor" parameterType="domain.blog.Author">
        update Author set
        username = #{username},
        password = #{password},
        email = #{email},
        bio = #{bio}
        where id = #{id}
</update>
 
<delete id="deleteAuthor” parameterType="int">
        delete from Author where id = #{id}
</delete>
```
                                             
(2)configuration 파일(SqlMapConfig.xml)
DB설정(별도의 properties파일로 분리가능)
mapper설정(SQL 쿼리를 xml로 분리한 것)



  ### MyBatis 구조
  ![mybatis구조](https://user-images.githubusercontent.com/46726709/107893887-f3121180-6f70-11eb-963e-3aac82ae1521.PNG)
  - Mybatis Component Flow<br>
  Mybatis Framework가 Business Layer(Persistance Layer + Service Layer)와 DB Layer 사이 가운데서 양쪽을 연결하고있다.
  mapper.xml 파일을 이용해 쿼리문을 별도로 작성한다. <br>

 
 ### 참조
 [MyBatis란 무엇인가?](https://m.blog.naver.com/PostView.nhn?blogId=wwwkang8&logNo=220989381100&proxyReferer=https:%2F%2Fwww.google.com%2F) <br>
 [MyBatis개요](https://www.youtube.com/watch?v=9b5P4YiyqOY&ab_channel=SKplanetTacademy) <br>
