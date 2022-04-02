# JSP&Servlet

## 특징

- 웹사이트를 구축하는 언어로 웹브라우저에서 동작하는 자바 문법(기술)
- 웹브라우저가 해석하지 못하기 때문에 해석용으로 WAS가 필요
- JSP는 마크업 중심 코드로 View, Servlet은 자바 중심 코드로 Controller 역할을 맡음
M - B/L, DAO, DTO=VO  |  V - HTML, CSS, JS, JSP  |  C - Servlet

# JSP

## 스크립팅 요소

```java
<%  기본 JSP 영역(스크립팅 릿)  %>

<%!  전역변수 선언 및 메소드선언  %>

<%=  출력문(out.println() 대신 사용)  %>

<%@
	문서 전체에 대한 설정 영역
	문서의 첫 줄에 기술하며 page지시어나 taglib을 선언함
%>

<%--  전체 주석처리  --%>
```

## 브라우저 출력

```java
out.print(문자열);
// 브라우저에 문자열 출력

out.println(문자열);
// 브라우저에 문자열 출력
// HTML 소스 상에서만 줄이 바뀌고 브라우저 상에서는 줄이 바뀌지 않음
```

## include

> top, footer 영역 등 많은 페이지에 동일한 형식으로 들어가는 영역을 따로 파일로 만들어 삽입하기 위해 사용
> 

```html
<!-- 스크립팅 요소로 include하기 -->
<%@ include file="url주소" %>
<!--
	WAS에서 변환될 때 소스가 하나의 페이지로 통합돼 Servlet이 하나만 만들어짐
	(=변수를 공유해 사용할 수 있음)
-->

<!-- 액션태그로 include하기 -->
<jsp:include page="url주소"></jsp:include>
<jsp:include page="url주소"/>
<!--
	모든 파일이 각각의 Servlet으로 생성된 후 하나로 합쳐짐
	(=변수 공유 불가)
-->
```

### 액션태그 include로 변수 받기

```html
<% request.setCharacterEncoding("UTF-8"); %> <!-- 인코딩 처리하지 않으면 한글이 깨짐 -->
<jsp:include page="url주소">
	<jsp:param value="값" name="변수명"/>
</jsp:include>
```

```java
<%
	request.getParameter("변수명");
	 // 보내온 파라미터 받기
%>
```

## WAS를 통한 이동

### forward

> 현재 request와 reponse를 유지하면서 이동하는 방식
페이지가 늘어나지 않고 현재 페이지에 포워딩됨(뒤로가기X)
> 

```html
<!-- 액션 태그로 포워드 -->
<% request.setCharacterEncoding("UTF-8"); %> <!-- 인코딩 처리하지 않으면 한글이 깨짐 -->
<jsp:forward page="url주소"></jsp:forward>
<jsp:forward page="url주소"/> <!-- 축약형 -->

<!-- 입력한 url주소 파일이 불러와지기 때문에 파일에 화면에 무언가를 출력해도 보이지 않음 -->
```

```java
/* 메소드 호출해 포워드(자바 코드) */
RequestDispatcher rd = request.getRequestDispatcher("url주소");
rd.forward(request, response)
```

```java
request.getParameter("변수명") // 보내온 파라미터 받기
```

### redirect

> 현재 request와 reponse를 버리고 새로운 request와 reponse를 생성해 이동하는 방식
> 

```java
response.sendRedirect("url주소");

// 이동할 때 넘겨주고 싶은 값이 있다면 주소에 수동 get 방식으로 넘겨줘야 함
response.sendRedirect("url주소?변수명=" + URLEncoder.encode(값, request.getCharacterEncoding()));
```

## JSP 내장객체

### HttpServletRequest: request

```java
javax.servlet.http.HttpServlerRequest;
// 클라이언트의 요청 정보를 서버에서 사용할 때 사용

String value = request.getParameter("name"); 
// request로 넘어오는 name의 value값 받기
  
request.setCharacterEncoding("인코딩");
// request로 넘어오는 인코딩 변환
    
String[] str = request.getParameterValues("name"); 
// name의 value값이 여러 개일 때 배열로 받기

Enumeration<String> e = request.getParameterNames();
// request로 넘어오는 name값 가져오기
      
String ip = request.getRemoteAddr(); 
// 접속한 클라이언트 ip 가져오기

Cookie co [] = request.getCookies();
// 접속한 클라이언트에 저장된 쿠키 정보(클라이언트 정보) 가져오기
```

```java
request.getContextPath();
// 서버에 올라간 컨텍스트 경로(프로젝트 구분 경로)를 가져옴

request.getRealPath(path);
// 접속한 문서의 절대경로를 가져옴
// path에 "/"를 입력하면 루트 경로를 가져옴

request.getRequestURL();
// 접속한 문서의 url 주소를 가져옴
```

### HttpServletResponse: response

```java
javax.servlet.http.HttpServletResponse
// 서버가 클라이언트 응답을 처리할 때 사용
    
response.sendRedirect("url 주소");
// 서버가 클라이언트 요청에 따라 url을 이동
// 이동할 때 넘겨주고 싶은 값이 있다면 주소에 수동 get 방식으로 넘겨줘야 함

response.addCookie(cookie);
// 클라이언트에 쿠키를 저장함

response.setContentType("인코딩");
// 클라이언트 한글 인코딩 설정

response.setStatus(code) ;
/*
	클라이언트쪽에 상태코드 설정
	200 : 정상(성공)
	400 : request 요청이 잘못되었을 때 (bad request) 발생
	403 : 인증은 했으나 권한이 부족할 때 발생
	404 : FileNotFoundException, 경로가 잘못되어 파일을 찾지 못할 때 발생
	405 : 요청방식 잘못되었을 때(get방식, post방식 구분하지 못했을 때) 발생
	500 : 소스코드 오류
*/

response.setError(code);
// 에러를 발생시킴
```

### HttpServletResponse: response

```java
HttpSession
/*
	클라이언트 정보를 서버에 저장할 때 사용
	저장된 정보는 브라우저 창이 유지되는 동안 유지됨(일반적으로 로그인 이후, 로그아웃 이전까지 유지)
	접속된 각각의 클라이언트마다 생성되며 기본 세션 시간은 30분(=1800초)
*/

session.setAttribute(name, value);
// 세션 정보 저장

Object value = session.getAttribute(name);
// 세션 정보를 가져옴

session.setMaxInactiveInterval(time);
// 세션이 유지되는 시간을 설정함
  
int interval = session.getMaxInactiveInterval(); 
// 설정된 세션 유지 시간을 가져옴

String id = session.getId();
// 세션이 생성되면 자동으로 만들어지는 세션아이디
 
Enumeration e = session.getAttributeNames();
// 세션에 저장된 name을 가져옴

boolean b = session.isNew();
// 현재 브라우저 창의 세션이 새 세션인지 구분(true: 새 페이지, false: 기존 페이지)

session.invalidate();
// 세션의 모든 정보를 지움

session.removeAttribute(java.lang.name);
// 저장된 세션 정보 중 name값이 같은 정보를 지움

long time = session.getLastAccessedTime();
// 마지막 접속 시간을 가져옴

long time = session.getCreationTime();
// 세션이 시작된 시간을 가져옴
```

### ServletContext: application

```java
ServletContext
/*
	특정 정보를 서버가 시작해서 종료될 때까지 유지시킴(반영구 유지)
	모든 유저의 정보가 공유됨
*/
     
application.setAttribute(name, value);
// 정보를 저장함
   
Enumeration e = application.getAttributeNames();
/*
	저장된 name값을 모두 가져옴
*/

application.getAttribute(name);
// name값이 같은 정보를 가져옴

application.removeAttribute(name);
// name값이 같은 정보를 삭제함

application.getRealPath(path);
// 실행된 문서의 경로를 가져옴
```

- AtomicInteger
    
    ```java
    /*
    	동기화 처리되어 application 등에 저장한 뒤 값이 변경되면 재저장하지 않아도 자동 변경됨
    */
    
    AtomicInteger ai = new AtomicInteger();
    // 새 AtomicInteger 객체를 만듦(초기값 0);
    
    ai.intValue();
    // 현재값을 가져옴
    
    ai.incrementAndGet();
    // 값을 1 증가시킴
    ```

### Cookie

```java
javax.servlet.http.Cookie
/*
	서버가 사용자 정보를 클라이언트 PC에 저장하는 기술
	한 번에 4kb, 총 300개 저장 가능
	일정 기간이 지나면 자동 삭제됨
*/

Cookie cookie = new Cookie("name","value");
// 새 쿠키 객체를 생성함(name과 value 모두 String 타입만 저장 가능)

cookie.getMaxAge();
// 쿠키 사용 가능 기간을 가져옴

cookie.setMaxAge(max)
/*
	쿠키 사용 가능 기간 설정(초 단위)
	매개변수로 0을 넣으면 쿠키가 삭제
	-1을 넣으면 파일 생성X 브라우저 실행 동안 쿠키 정보 저장(종료 시 사라짐)
*/

cookie.setValue(cookie);
// 쿠키 정보 수정(수정 시 setMaxAge 초기화)

cookie.getName();
// 쿠키에 설정된 name값 가져오기

cookie.getValue();
// 쿠키에 설정된 value값 가져오기 

cookie.setPath(path)
/*
	쿠키의 유효 디렉토리(쿠키 사용 가능 영역) 설정
	매개변수로 "/"를 넣을 경우 모든 문서에서 쿠키 사용 가능
*/
```

```java
response.addCookie(Cookie co);
// 클라이언트에 정보 저장

Cookie co [] = request.getCookies();
// 클라이언트에 저장된 정보 모두 가져옴
```

### exception

```java
// 문서 첫 줄에 errorPage="" 설정해 오류 발생 시 에러 페이지로 이동하는 방법

<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" errorPage="에러페이지 url경로"%>
/*
	페이지에서 일어나는 모든 에러를 한 번에 처리할 수 있지만 에러 페이지를 하나만 사용할 수 있음
	web.xml 문서 설정과 함께 사용할 때 이 방법이 우선순위가 높음
	(=둘 다 설정할 경우 이 방법이 실행됨)
*/
```

```xml
<!-- web.xml 문서에 설정하는 방법 -->

<error-page>
	<exception-type>처리할 exception 종류</exception-type>
	<location>이동할 에러페이지</location>
</error-page>
<!--
	처리할 exception 종류는 자동완성이 안되기 때문에 패키지명까지 수동 입력
	이동할 에러페이지는 보통 루트에서 시작함: / = webapp
	web.xml 문서는 서버가 시작할 때 한 번만 로딩되기 때문에 수정한 뒤에는 서버를 재시동해야 적용됨
-->
```

```java
// jsp 문서 에러 관련 메소드 사용 방법

<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" isErrorPage="true"%>
<%
	response.setStatus(200);
%>
/*
	isErrorPage="true" 설정하지 않으면 exception 레퍼런스 사용 불가
	설정할 경우 해당 페이지의 상태코드가 500으로 고정돼 브라우저에 따라 출력되지 않을 수 있음
	이를 방지하기 위해 response.setStatus() 메소드 사용해 상태코드를 200으로 변경
*/
```

# Servlet

## 문서 작성 및 사용 방법

### 문서 작성

```java
public class 클래스명 extends HttpServlet { }
// 반드시 public class여야 하며, HttpServlet 상속받아 필요한 메소드를 재정의해 작성함
```

### 문서 사용

- web.xml 문서 설정

```xml
<!-- 서블릿 개체 생성 -->
<servlet>
	<servlet-name>서블릿 개체명 설정</servlet-name>
	<servlet-class>자바 파일 경로</servlet-class>
	<load-on-startup>n(제작 순서)</load-on-startup>
	<!-- load-on-startup 옵션을 설정하면 tomcat이 start될 때 미리 생성함 -->
</servlet>

<!-- 생성한 서블릿을 url에서 호출 -->
<servlet-mapping>
	<servlet-name>서블릿 개체명</servlet-name>
  <url-pattern>url 주소 설정(루트 기준)</url-pattern>
</servlet-mapping>
```

- @annotation 설정

```java
public class 클래스명 extends HttpServlet { }
// 반드시 public class여야 하며, HttpServlet 상속받아 필요한 메소드를 재정의해 작성함
```

## 웹페이지 구성

```java
// Servlet으로 웹페이지 문서를 만들기 위해서는 jsp와 달리 아래처럼 직접 마크업을 입력해야 함

// 문자 인코딩 처리
response.setContentType("text/html;charset=UTF-8");
		
// 브라우저 출력
PrintWriter out = response.getWriter();

out.println("<html>");
out.println("<head><title>servlet</title></head>");

out.println("<body>");
out.println("<h1>빰빰빰</h1>");
out.println("<h1>nununu</h1>");
out.println("</body>");

out.println("</html>");
```

## 기본 메소드

```java
init();
/*
	서블릿 문서가 초기화될 때 최초에 자동으로 실행됨
	생성자와 비슷하게 객체가 생성된 후 반드시 해야 할 일이 있을 때 오버라이딩해 사용함
*/

service(ServletRequest request, ServletResponse response);
/*
	init이 실행된 후 호출됨(사용자 요청이 들어오면=새로고침되면 호출)
	사용자 요청이 get 방식인지 post 방식인지 구분해 doGet() | doPost() 메소드를 호출함
	요청방식에 상관없이 기능을 만들 경우 오버라이딩해 사용
*/

doGet(HttpServletRequest request , HttpServletResponse response);
/*
	사용자 요청이 get 방식일 경우 실행됨
	요청방식을 구분해 기능을 만들 경우 오버라이딩해 사용
*/

doPost(HttpServletRequest request , HttpServletResponse response);
/*
	사용자 요청이 post 방식일 경우 실행됨
	요청방식을 구분해 기능을 만들 경우 오버라이딩해 사용
*/

destory();
/*
	서블릿 문서가 종료될 때(=메모리에서 소멸될 때) 호출됨
	종료할 때 반드시 해야 할 일이 있을 때 오버라이딩해 사용함
*/
```