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
|mapping파일 (user.xml) |SQL문과 OR Mapping 설정 |
|SqlSessionFactoryBuilder|MyBatis설정 파일을 바탕으로 SqlSessionFactory를 생성한다.|
|SqlSessionFactory|SqlSession을 생성한다|
|SqlSession|핵심적인 역할을 하는 클래스. SQL 실행이나 트랜잭션 관리를 실행. thread-safe하지 않으므로 thread마다 필요시 생성|

### 1. MyBatis 환경설정파일 (SqlSessionConfig.xml)
1. TypeAlias 설정 : 사용할 모델 클래스에 대한 별칭 설정 <typeAlias>
2. DB연동을 위한 설정: DataBase에 어떻게 접속할 것인지에 대한 설정 <environment>. 별도의 properties 파일로 분리 가능
3. Mapper 설정파일 등록: 매핑 설정이 어디있는지 <mapper>
- ex. SpringMVC 프로젝트는 root-context.xml에서 설정하기도함
```xml
  	<!-- 커넥션 풀 DataSource 객체 데이터베이스 접속 설정 -->
	<bean id="dataSource" destroy-method="close"
		class="org.apache.commons.dbcp.BasicDataSource"
		p:driverClassName="oracle.jdbc.driver.OracleDriver"
		p:url="jdbc:oracle:thin:@localhost:1521:testdb" p:username="hr"
		p:password="hr" />

	<!-- MyBatis 환경설정파일 -->
	<bean id="sqlSessionFactory"
		class="org.mybatis.spring.SqlSessionFactoryBean">
		<property name="dataSource" ref="dataSource" />  <!-- DB설정(별도의 properties파일로 분리가능) -->
		<!-- 아래부분은 매핑할 xml파일이 있는 패키지경로를 설정한다. -->
		<property name="typeAliasesPackage" value="spring.model" />
		<property name="mapperLocations"
			value="classpath:mybatis/*.xml" />
	</bean>

	<bean id="sqlSession"
		class="org.mybatis.spring.SqlSessionTemplate">
		<constructor-arg name="sqlSessionFactory"
			ref="sqlSessionFactory" />
	</bean>

	<!-- mapper xml Mapper Interface설정 -->
	<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
		<property name="basePackage" value="spring.model" />
	</bean>
```

### 2. Mapper 파일 (user.xml, person.xml)
1. 두가지 종류.
  - SQL을 XML에 정의된 XML로 생성
  - SQL을 메소드에 어노테이션으로 정의한 인터페이스로 생성
2. 구성 요소
  - SQL문 태그의 구성요소 ( id, ParameterType, ResultType, SQL문)
    - id 속성 : 필수속성으로 전체 Mapper파일들 내에서 유일한 아이디 등록
    - Mapper루트태그(<Mapper namespace="">)의 namespace가 다르면 같은 id도 다른 id로 인식된다.
    - parameterType 속성 : 외부로부터 데이터를 받아올 때 사용. insert, update시 사용할 데이터를 받아와서 생성,수정
    - resultType 속성 : 주로 select 구문 처리 후 DBMS로부터 결과를 받아올 때 사용. 결과값을 매핑할 자바 객체 타입을 명시한다. select 구문에서 필수
  - SQL태그 : insert, delete, update, select
  
3. mapper파일 선언

```xml
<!DOCTYPE mapper
PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="bbs"> 
</mapper>
  ```
  - Mapper구조는 DTD선언 밑에 <mapper>루트 엘리먼트가 선언.
  - mapper 엘리먼트는 namespace속성을 가진다
4. 활용 <br>
   4-1. select <br>
   select 구문은 resultType이 필수다.
```xml
   <select id=”selectPerson” parameterType=”int” resultType=”hashmap”>
      SELECT * FROM PERSON WHERE ID = #{id}
    </select>
```
   4-2. insert, update, delete <br> 
  - insert의 selectKey는 기본 키 필드의 자동생성을 지원
  - <selectKey>를 사용하면 생성된 키를 쉽게 가져올 수 있다.
```xml
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
  4-3. resultMap 속성 <br>
- 결과를 매핑할 때 하나의 java객체로 매핑이 안되는 경우에 사용(join)등
- 테이블 컬럼명과 매핑할 자바 객체의 필드명이 다를 때도 사용
<resultMap>의 매핑규칙을 지정한다.
```xml
 <resultMap id="selectResult" type="board">
     <result property="num" column = 'seq'>
     <result property="title" column = 'subject'>
     <result property="content" column = 'content'>
     <result property="redate" column = 'redate'>
</resultMap>
<select id=”selectBoard” parameterType=”int” resultMap=”selectResult”>
    SELECT * FROM board WHERE num = #{num}
</select>
```
   4-4. CDATA <br>
- SQL 구문에 '<'를 사용하면 에러가 난다. (xml파서가 <를 태그 시작으로 처리)
- CDATA 구역을 만들어 단순 문자 데이터로 인식하게 하여 에러를 피한다.
```xml
<select id=”selectBoard” parameterType=”int” resultType=”board”>
    SELECT *
    FROM board
   <![CDATA[
    WHERE num <= #{num}
    ]]>
</select>
```
  4-5. 동적 SQL <br>
  - if,choose,when,otherwise, where, set, foreach 등 사용
  - choose, when, otherwise는 else문처럼 사용
  - <set>,<where> 태그는 단순히 set,where만 추가. 조건문을 사용하면 일부 문법적 오류가 날 수 있는부분(AND나 OR, 콤마 등)을 처리해줌
 ```xml
<select id=”findActiveBlogLike”
        parameterType=”Blog” resultType=”Blog”>
        SELECT * FROM BLOG
        <where>
        <if test=”state != null”>
                state = #{state}
        </if>
        <if test=”title != null”>
                AND title like #{title}
        </if>
        <if test=”author != null and author.name != null”>
                AND author_name like #{author.name}
        </if>
        </where>
</select>
```
   - foreach 는 컬렉션에 대해 반복처리한다. 
```xml
  <select id="selectPostIn" resultType="domain.blog.Post">
        SELECT *
        FROM POST 
        WHERE ID in 
        <foreach item="item" index="index" collection="list"
        open="(" separator="," close=")">
                #{item}
        </foreach>
</select>
```
  |구분|설명|
|---------|--------|
|collection|전달받은 인자값|
|item|전달받은 인자값을 다른이름으로 대체
|open|해당 구문이 시작할 때|
|close|해당 구문이 끝날 때|
|index|항목의 인덱스 값을 꺼낼 때 사용할 변수 이름을 지정|
|seperator|구분자. 한번 이상 반복되면 사이에 해당 구분자를 넣어줌|
```xml
<select id="selectPostIn" resultType="domain.blog.Post">
        SELECT *
        FROM POST 
        WHERE ID in 
        <foreach item="item" index="index" collection="list"
        open="(" separator="," close=")">
                #{item}
        </foreach>
</select>
```



  ### MyBatis 구조
  ![mybatis구조](https://user-images.githubusercontent.com/46726709/107893887-f3121180-6f70-11eb-963e-3aac82ae1521.PNG)
  - Mybatis Component Flow<br>
  Mybatis Framework가 Business Layer(Persistance Layer + Service Layer)와 DB Layer 사이 가운데서 양쪽을 연결하고있다.
  mapper.xml 파일을 이용해 쿼리문을 별도로 작성한다. <br>

 
 ### 참조
 [MyBatis란 무엇인가?](https://m.blog.naver.com/PostView.nhn?blogId=wwwkang8&logNo=220989381100&proxyReferer=https:%2F%2Fwww.google.com%2F) <br>
 [MyBatis개요](https://www.youtube.com/watch?v=9b5P4YiyqOY&ab_channel=SKplanetTacademy) <br>
 [스프링,Mybatis,MySQL연동](https://codevang.tistory.com/249)<br>
