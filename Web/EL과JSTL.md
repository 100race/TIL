# EL과 JSTL
  ## 1. EL(Expression Language)
  ### 1-1. EL이란
  JSP의 출력 언어를 대체하는 표현 언어. JSP파일에 자바형식 코드를 사용할 때의 불편한 점을 해결할 수 있고 가독성을 높여주며 코드가 간결해진다. 
 
  - JSP에서의 값 표기법, i는 변수다.
   ```
   <%=i %>
   ```
  - EL에서의 값 표기법, i는 이름이다.
   ```
   ${ i }
   ```
  - 찾고자하는 attribute 이름이 같을 경우, scope가 작은 범위에서 큰 범위로 이름이 존재하는지 찾는다. <br>
   (page -> request -> session -> application) <br>
   만약 request scope와 session scope에 동일한 A attribute가 있다면 ${A}의 결과는 request scope의 값을 출력
   
   - attribute란? : 메소드를 통해 저장되고 관리되는 데이터 <br>
   setAttribute("key",value), getAttribute("key"), removeAttribute("Key") 등이 PageContext, Request, Session등에서 사용됨
   
   ### 1-2. EL언어의 사용
   #### 연산자
   - 우선순위 연산자 (), .연산자, 배열연산자 [], x?a:b 삼항연산자, 산술연산자, 논리연산자, 비교연산자는 기존과 같으며 추가적으로 영단어로 표현 가능하다. [참고](https://sinpk.tistory.com/entry/JSP-EL-%ED%91%9C%EA%B8%B0%EB%B2%95)
   - empty 연산자 존재. ${empty 데이터명}을 하면 값이 null일 경우 true를 반환
   #### 내장객체
   - EL표기법은 내장객체를 제공
   - 파라미터의 값은 param키워드를 통해 가져온다.
   - JSP 값 표기법에서 파라미터는 문자열이지만 EL은 숫자는 숫자로 인식한다.
   ```
   <%= request.getParameter("a") + 100 %>    JSP => 10100
   ${param.a + 100 }                           EL  => 110
   ```
   - 자주 사용되는 객체. {}은 기본적으로 request에 접근한다. 
   
   |객체|사용|
   |------|------|
   |pageScope|페이지 scope접근|
   |requestScope|리퀘스트 scope접근|
   |sessionScope|세션 scope 접근|
   |applicationScope|어플리케이션 scope접근|
   |param|파라미터값 1개 얻어올때|
   |paramValues|파라미터값 배열로 얻어올때|
   |header|헤더값 1개 얻어올때|
   |headerValues|헤더값 배열로 얻어올때|
   |cookie|${cookie.key값.value값}으로 쿠키값 조회|
   |initParam|초기파라미터 조회|
   |pageContext|페이지컨텍스트 객체를 참조|
   
   - 배열값으로 받아온 값 쓰는법 예시
   ```
   ${paramValues.bbsDto[0]} 또는 ${paramValues["bbsDto"][1]}
   ```

  
  
  ## 2. JSTL(Jsp Standard Tag Library)
  태그<>를 통해 JSP코드를 관리하는 라이브러리로 JSP의 가독성을 높이고 DB를 편하게 처리. 라이브러리이기 때문에 사용하기 위해서는 추가해야한다. 추가 시 
  <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%> 이런식으로 선언하는데 uri와 prefix를 사용할 태그에 맞게 추가해준다.
  
  2-1.태그의 종류 <br>
  태그의 종류에는 core, format, function, xml, sql

- Core (prefix:c) : 흐름제어, 일반프로그래밍의 변수선언과유사, 페이지 이동기술 제공 <br>
   uri =  http://java.sun.com/jsp/jstl/core

- Formatting (prefix:fmt) : 숫자, 날짜, 시간을 포맷팅. <br>
    uri = http://java.sun.com/jsp/jstl/fmt

- Database (prefix:sql) : DB데이터를 crud 할 수 있는 기능을 제공<br>
   uri = http://java.sun.com/jsp/jstl/sql

- XML (prefix:x) : XML문서를 처리할 때 필요한 기능 제공 <br>
   uri = http://java.sun.com/jsp/jstl/xml

- Function (prefix:fn) : 문자열을 제공하는 함수 제공 <br>
   uri = http://java.sun.com/jsp/jstl/functions


  2-2. JSTL 태그의 속성
  1. set : 변수 생성
  ```
  <c:set var="변수명" value="값" [scope="변수저장영역"]/>
  <c:set var="count" value="${fn:length(list)}"/>
  ```
  2. if : 하나의 if문을 나타냄
  ```
  <c:if test="${col=='total' }">selected</c:if>
  ```
  3. choose : else if문을 나타냄. choose - when(if) - otherwise(else). test는 조건을 나타냄.
  ```
   <c:choose>
  <c:when test="${empty list}">
   <tr><td colspan="6">등록된 글이 없습니다.</td>
  </c:when>
  <c:otherwise>
    <td>${dto.bbsno}</td>
  </c:otherwise>

   ```
  4. foreach
  ```
  <c:forEach var="변수" begin="1" end="${dto.indent }" items="${아이템} step="증가값" varStatus="변수명지정">&nbsp;&nbsp;</c:forEach>
  ```
  5. split
  ```
  <c:set var="phone" value="${ fn:split(userVO.phone , '-') }" />
  ```

## 3. EL JSTL 적용 전 후
  - EL JSTL은 가독성을 높여주고 퍼블리셔와 협업시 java코드를 줄여 보기 편하게 만들 수 있다.
  - 적용 전 게시판 list.jsp
```
<%@ page contentType="text/html; charset=UTF-8" %>
<%@ include file="/ssi/ssi_bbs.jsp" %>
<%
List<BbsDTO> list = (List<BbsDTO>)request.getAttribute("list");
String paging = (String)request.getAttribute("paging");
String col = (String)request.getAttribute("col");
String word = (String)request.getAttribute("word");
int nowPage = (Integer)request.getAttribute("nowPage");
%> 

<!DOCTYPE html> 
<html> 
<head>
  <title>Bootstrap Example</title>
  <meta charset="utf-8">
   <script type="text/javascript">
     function read(bbsno){
       var url = "read";
       url += "?bbsno="+bbsno;
       url += "&col=<%=col%>";
       url += "&word=<%=word%>";
       url += "&nowPage=<%=nowPage%>";
       location.href=url;

     }
  
  </script>

</head>
<body>
<div class="container">

  <h2>게시판 목록</h2>
  <form class="form-inline" action="./list">
    <div class="form-group">
      <select class="form-control" name="col">
        <option value="wname"
        <% if(col.equals("wname")) out.print("selected");%>
        >성명</option>
        <option value="title"
        <% if(col.equals("title")) out.print("selected");%>
        >제목</option>
        <option value="content"
        <% if(col.equals("content")) out.print("selected");%>
        >내용</option>
        <option value="title_content"
         <% if(col.equals("title_content")) out.print("selected");%>
        >제목+내용</option>
        <option value="total"
        <% if(col.equals("total")) out.print("selected");%>
        >전체출력</option>       
     </select>
    </div>
    <div class="form-group">
      <input type="text" class="form-control" placeholder="Enter 검색어" 
      name="word" value="<%=word%>">
    </div>
    <button type="submit" class="btn btn-default" >검색</button>
    <button type="button" class="btn btn-default" onclick="location.href='./create'">등록</button>
  </form>
  
  <table class="table table-striped">
   <thead>
    <tr>
    <th>번호</th>
    <th>제목</th>
    <th>작성자</th>
    <th>grpno</th>
    <th>indent</th>
    <th>파일</th>
    </tr>
   </thead>
   <tbody>
   

<%if(list.size() ==0){ %> 
   <tr><td colspan="6">등록된 글이 없습니다.</td>

<%}else{
  
   for(int i=0; i<list.size();i++){
      BbsDTO dto = list.get(i);
      
%> 
   <tr>
    <td><%=dto.getBbsno() %></td>
    <td>
      <%
       for(int r=0; r<dto.getIndent(); r++){
              out.println("&nbsp;&nbsp;");
       }
       if(dto.getIndent()>0)
           // out.print("[답변]");
               out.print("<img src='../images/re.jpg' >");
       %>

   
    <a href="javascript:read('<%=dto.getBbsno() %>')"><%=dto.getTitle() %></a>
    <% if(Utility.compareDay(dto.getWdate().substring(0,10))){ %> 
    <img src="../images/new.gif"> 
    <% } %> 
    
    </td>
    <td><%=dto.getWname() %></td>
    <td><%=dto.getGrpno() %></td>
    <td><%=dto.getIndent() %></td>
    <td><%if(dto.getFilename()!=null){ %>
            <%=dto.getFilename() %>
      <%} %>
    </td>
   </tr>
<%  
   } //for_end
   
  } //if_end
%>  
   </tbody>
  
  </table>
  <div>
      <%=paging %>
  </div>
</div>
</body> 
</html> 

  ```
  - 적용 후 게시판 list.jsp
  ```
  <%@ page contentType="text/html; charset=UTF-8" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ include file="/ssi/ssi_bbs.jsp" %>
<!DOCTYPE html> 
<html> 
<head>
  <title>Bootstrap Example</title>
  <meta charset="utf-8">
   <script type="text/javascript">
     function read(bbsno){
       var url = "read";
       url += "?bbsno="+bbsno;
       url += "&col=${col}";
       url += "&word=${word}";
       url += "&nowPage=${nowPage}";
       location.href=url;
     }
  
  </script>

</head>
<body>
<div class="container">

  <h2>게시판 목록</h2>
  <form class="form-inline" action="./list">
    <div class="form-group">
      <select class="form-control" name="col">
        <option value="wname"
        <c:if test="${col=='wname' }">selected</c:if>
        >성명</option>
        <option value="title"
        <c:if test="${col=='title' }">selected</c:if>
        >제목</option>
        <option value="content"
       <c:if test="${col=='content' }">selected</c:if>
        >내용</option>
        <option value="title_content"
         <c:if test="${col=='title_content' }">selected</c:if>
        >제목+내용</option>
        <option value="total"
        <c:if test="${col=='total' }">selected</c:if>
        >전체출력</option>       
     </select>
    </div>
    <div class="form-group">
      <input type="text" class="form-control" placeholder="Enter 검색어" 
      name="word" value="${word}">
    </div>
    <button type="submit" class="btn btn-default" >검색</button>
    <button type="button" class="btn btn-default" onclick="location.href='./create'">등록</button>
  </form>
  
  <table class="table table-striped">
   <thead>
    <tr>
    <th>번호</th>
    <th>제목</th>
    <th>작성자</th>
    <th>grpno</th>
    <th>indent</th>
    <th>파일</th>
    </tr>
   </thead>
   <tbody>
 <c:choose>
  <c:when test="${empty list}">
   <tr><td colspan="6">등록된 글이 없습니다.</td>
  </c:when>
  <c:otherwise>
  <c:forEach var="dto" items="${list}">
   <tr>
    <td>${dto.bbsno}</td>
    <td>
      <c:forEach begin="1" end="${dto.indent }">&nbsp;&nbsp;</c:forEach>
      <c:if test="${dto.indent >0 }"><img src='../images/re.jpg' ></c:if>
    <a href="javascript:read('${dto.bbsno}')">${dto.title}</a>
    <%--if(Utility.compareDay(dto.getWdate().substring(0,10))){ --%> 
    <img src="../images/new.gif"> 
    <%-- } --%> 
    
    </td>
    <td>${dto.wname}</td>
    <td>${dto.grpno}</td>
    <td>${dto.indent}</td>
    <td>${dto.filename}</td>
   </tr>
   </c:forEach>
 </c:otherwise> 
</c:choose>
   </tbody>
  </table>
  <div>
      ${paging}
  </div>
</div>
</body> 
</html>

  ```
  
  
  
  
  
  ### 참조
  [EL과 JSTL](https://hunit.tistory.com/203)<br>
  [JSTL과 EL](https://victorydntmd.tistory.com/156)<br>
