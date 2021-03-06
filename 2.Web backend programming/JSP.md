- 모든 jsp는 servlet으로 바뀌어서 동작
- `<%@ page` page 지시자
- `<%=abc %>` 표현식, 응답 결과 보여주는 부분 `== out.print(abc);`

### JSP 등장 배경

- JSP는 실제로 서블릿 기술 사용!!! (바뀐 후 실행)

### JSP 라이프 사이클

sum10.jsp가 실행될 때 벌어지는 일

- 이클립스 workspace 아래의 .metadata 폴더에 sum10_jsp.java파일 생성
- 해당 파일의 _jspService() 메소드 안을 보면 jsp파일의 내용이 변환돼서 들어가 있음
- `\*\* sum10_jsp.java`는 서블릿 소스로 자동으로 컴파일, 실행 -> 결과가 브라우저에 보여짐

### JSP의 실행 순서

1. 브라우저가 웹서버에 JSP에 대한 요청 정보 전달
2. 브라우저가 요청한 JSP가 '최초로' 요청했을 경우만
- JSP로 작성된 코드가 서블릿 코드로 변환 (java 파일 생성)
- 서블릿 코드를 컴파일해서 실행 가능한 bytecode로 변환 (class 파일 생성)
- 서블릿 클래스를 로딩, 인스턴스 생성 -> jsp엔진이
1. 서블릿이 실행되어 요청 처리, 응답 정보 생성

### JSP 문법

스크립트 요소의 이해
선언문(Declaration) `<%! 문장 %>`

- 전역변수 선언 및 메소드 선언에 사용
- JSP 페이지 내에서 필요한 멤버변수나 메소드가 필요할 때 선언해 사용하는 요소

```java
id : <%=getId() %>
<%!
String id = "u001"; //멤버변수 선언
public String getId(){ //메소드 선언
return id;
}
%>
```

스크립트릿(Scriptlet) `<% %>`

- 프로그래밍 코드 기술(로직 기술)에 사용
- 가장 일반적으로 많이 쓰임
- 선언된 변수는 지역변수
- Service 안에서 실행

```java
<%
for(int i=1; i<=5; i++){
%>
<H<%=i %>> 아름다운 한글</H<%=i %>>
<%
}
%>
표현식(Expression) <%= %>
```

- 화면에 출력할 내용(응답 결과에 포함할 내용) 기술에 사용
- 스크립트릿 내에서 출력할 부분은 out객체의 print() 또는 println() 메소드 사용해서 출력

주석(Comment)

- html 주석, 자바 주석, JSP 주석(servlet으로 안바뀜)
HTML 주석 <!-- 문장 -->
- HTML 주석을 사용한 페이지를 웹에서 서비스할 때 화면에 주석 내용이 표시되지 않지만 [소스보기]수행하면 주석의 내용이 화면에 표시

JSP 주석 <%-- 문장 --%>

- JSP 페이지에서만 사용
- 해당 페이지를 웹 브라우저를 통해 출력 결과로서 표시하거나 웹 브라우저 상에서 소스보기를 해도 표시되지 않음
- 주석 내에 실행코드를 넣어도 그 코드는 실행되지 않음
자바주석 //, /* */*

    ```java

    *<%-- jsp주석입니다!!!
    여러줄로 사용 가능
    --%>
    <!-- html 주석입니다 -->
    <%
    //자바 주석 입니다.
    for(int i=1; i<=5; i++){
    %>
    <H<%=i %>> 아름다운 한글</H<%=i %>>
    <%
    /*
    ㅁ
    ㄹㅇ
    /
    }
    %>
    ```

### JSP 내장객체(Implicit Objects)

- JSP를 실행하면 서블릿 소스가 생성되고 실행된다.
- JSP에 입력한 대부분의 코드는 생성되는 서블릿 소스의 _jspService() 메소드 안에 삽입되는 코드로 생성됨
- _jspService()에 삽입된 코드의 윗 부분에 미리 선언된 객체들이 있는데, 해당 객체들은 jsp에서도 사용 간으
- response, request, application, session, out과 같은 변수가 내장객체
- 선언 없이 사용 자바코드 내(스크립트릿) 사용 가능
