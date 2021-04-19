# SpringMVC 구조
![springmvc구조](https://user-images.githubusercontent.com/46726709/110488901-44598f00-8132-11eb-87c4-a3a5e2844b2c.PNG)<br>

1. DispatcherServlet <br>
- 서블릿 클래스. 모든 클라이언트의 요청을 처리한다.
- Controller(Action)에게 클라이언트의 요청을 전달하고, 컨트롤러가 리턴한 결과값을 View에 전달하여 알맞은 응답을 생성하도록 한다.
2. HandlerMapping 
- 클라이언트의 요청 URL을 어떤 Controller(Action)이 처리할지 결정
- 요청 URL과 Controller 클래스의 맵핑을 관리
3. Controller(Action)
- 클라이언트의 실질적인 요청을 처리
- 처리 결과를 Model에 담아서 DispatcherServlet에 반환
4. Model
- Controller(Action)가 처리한 모델의 결과 정보를 담는다
5. ViewResolver
- Controller(Action)의 처리 결과를 생성할 뷰를 결정
- Controller가 리턴한 뷰 이름, (뷰네임)으로 실행될 JSP 경로 완성
6. View
- Controller(Action)의 처리 결과 화면, 출력 데이터를 설정




# SpringMVC 처리순서
1. 클라이언트가 서버에 요청하면 DispatcherServlet이 요청을 받아 Controller에 보낸다.

DispatcherServlet(프로젝트 파일 내의 /WEB-INF/spring/appServlet/servlet-context.xml) 이
HandlerMapping에 클라이언트의 요청 URL을 어떤 Controller가 처리할지 물어본다

2. HandlerMapping은 요청에 매핑된 컨트롤러를 가 있다면 @Controller에 정의된 @RequestMapping(또는 Post,Get..)을 통해 요청을 처리할 메소드로 이동한다.
```java
@Controller
public class HomeController {
	
	private static final Logger logger = LoggerFactory.getLogger(HomeController.class);
	
	/**
	 * Simply selects the home view to render by returning its name.
	 */
	@RequestMapping(value = "/", method = RequestMethod.GET)
	public String home(Locale locale, Model model) {
		logger.info("Welcome home! The client locale is {}.", locale);
		
		Date date = new Date();
		DateFormat dateFormat = DateFormat.getDateTimeInstance(DateFormat.LONG, DateFormat.LONG, locale);
		
		String formattedDate = dateFormat.format(date);
		
		model.addAttribute("serverTime", formattedDate );
		
		return "/home";
	}
	
}
```
3. Controller는 해당요청을 처리할 Service를 주입(DI)받고 Service에 요청에 필요한 작업을 위임한다. 
```java 
//컨트롤러에 주입된 서비스
@Autowired
	private BbsService service;
```
4. Service는 요청에 필요한 작업을 담당, DB에 필요한 작업이 있으면 DAO를 주입받아 DAO에 DB처리를 위임한다. 

5. DAO는 mybatis(또는 hibernate등) 설정을 이용해 SQL쿼리를 날려 DB정보를 DTO에 받아 Service에 전달

6. Service는 전달받은 결과 데이터를 Controller에 전달

7. Controller는  Model(모델) 객체에 결과물 넣거나, 어떤 View(jsp)를 보여줄지 정보를 담아 DispatcherServlet에 전송

8. Dispatcher는 ViewResolver에 View정보를 전달

9. ViewResolver는 View에 대한 JSP(화면)를 찾아 DispatcherServlet에 전달

10. DispatcherServlet은 응답할 뷰의 렌더링 요청, View는 화면 렌더링 로직 처리

11. DispatcherServelt은 클라이언트에 렌더링된 View 응답.


# DispatcherServlet, 스프링 컨텍스트 설정 및 한글처리
서블릿 컨테이너 설정파일인 web.xml에 세 정보를 설정한다.
1. 클라이언트의 요청을 전달받을 DispatcherServlet설정
2. 공통으로 사용할 어플리케이션 컨텍스트 설정
3. 한글 처리용 필터 설정

```xml
>>> web.xml
<?xml version="1.0" encoding="UTF-8"?> 
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
xmlns="http://java.sun.com/xml/ns/javaee"  
xmlns:web="http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"  
xsi:schemaLocation="http://java.sun.com/xml/ns/javaee  
http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" version="2.5"> 
  <!--2.-->
  <context-param> 
    <param-name>contextConfigLocation</param-name> 
    <param-value>/WEB-INF/spring/root-context.xml</param-value> 
  </context-param> 
  <listener> 
    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class> 
  </listener> 
  <!--1.-->
  <servlet> 
    <servlet-name>appServlet</servlet-name> 
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class> 
    <init-param> 
      <param-name>contextConfigLocation</param-name> 
      <param-value> 
      /WEB-INF/spring/appServlet/dispatcher-servlet.xml              
      </param-value> 
    </init-param> 
    <load-on-startup>1</load-on-startup> 
  </servlet> 
  <servlet-mapping> 
    <servlet-name>appServlet</servlet-name> 
    <url-pattern>/</url-pattern> 
  </servlet-mapping>
  <!--3.-->
  <filter> 
<filter-name>encodingFilter</filter-name> 
<filter-class> 
org.springframework.web.filter.CharacterEncodingFilter 
</filter-class> 
<init-param> 
<param-name>encoding</param-name> 
<param-value>UTF-8</param-value> 
</init-param> 
  </filter> 

  <filter-mapping> 
<filter-name>encodingFilter</filter-name> 
<url-pattern>/*</url-pattern> 
  </filter-mapping> 
  <welcome-file-list> 
    <welcome-file>index.jsp</welcome-file> 
  </welcome-file-list> 
</web-app>
```



### 참조 
[spring구조 이해및처리](https://iri-kang.tistory.com/4)<br>
[spring mvc 처리과정](https://jeong-pro.tistory.com/96)<br>
