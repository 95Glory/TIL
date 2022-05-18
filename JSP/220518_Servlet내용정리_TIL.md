# 22.05.18 Servlet 수업 내용정리:pencil2:
## 1. 서블릿 이란?:pushpin:

**서블릿이란 동적Web Page를 만들 때 사용되는 자바 기반의 웹 애플리케이션 프로그래밍 기술이다.**  
 웹을 만들때는 다양한 요청(Request)과 응답(Response)이 있기 마련이고 이 요청과 응답에는 규칙이 존재한다. 이러한 요청과 응답을 일일이 처리하려면 굉장히 번거로울것이다. **서블릿은 이러한 웹 요청과 응답의 흐름을 간단한 메서드 호출만으로 체계적으로 다룰 수 있게 해주는 기술이다.**    
 
서블릿은 **자바 클래스로 웹 애플리케이션을 작성한 뒤 이후 웹 서버 안에 있는 웹 컨테이너에서 이것을 실행**하고, **웹 컨테이너에서는 서블릿 인스턴스를 생성 후 서버에서 실행되다가 웹 브라우저에서 서버에 요청(Request)을 하면 요청에 맞는 동작을 수행**하고 웹 브라우저에 HTTP형식으로 응답(Response) 한다.  

### [Servlet의 주요특징]
-   클라이언트의 Request에 대해 동적으로 작동하는 웹 애플리케이션 컴포넌트
-   HTML을 사용하여 Response 한다.
-   MVC 패턴에서의 컨트롤러로 이용된다.
-   HTTP 프로토콜 서비스를 지원하는 javax.servlet.http.HttpServlet 클래스를 상속받는다.
-   HTML 변경 시 Servlet을 재 컴파일해야 하는 단점이 있다.

### [Servlet Container]

**서블릿 컨테이너란 말 그대로 서블릿을 담고 관리해주는 컨테이너입니다.** 서블릿 컨테이너는 구현되어 있는 servlet 클래스의 규칙에 맞게 서블릿을 관리해주며 클라이언트에서 요청을 하면 컨테이너는 HttpServletRequest, HttpServletResponse 두 객체를 생성하며 post, get여부에 따라 **동적인 페이지를 생성하여 응답을 보낸다.**

### [Servlet의 동작과정]
**1.  Servlet Request, Servlet Response 객체를 생성**

**2.  설정 파일을 참고하여 매핑할 Servlet을 확인**

**3.  해당 서블릿 인스턴스 존재의 유무를 확인하여 없으면 init() 메소드를 호출하여 생성**

**4.  Servlet Container에 스레드를 생성하고 service를 실행**

**5. 응답을 처리하였으면 distory() 메소드를 실행하여 Servlet Request, Servlet Response 객체를 소멸**

### [Cookie 와 Session]

**Cookie 란?**
쿠키는 대부분의 웹사이트에서 사용되며, 쿠키란 **사용자의 컴퓨터 및 모바일 장치에 설치되는 작은 텍스트 조각**  
 이러한 쿠키는 당사의 웹사이트로 다시 보내지거나, 쿠키를 인식하는 기능이 있는 다른 웹사이트로 전송된다고 한다.

쿠키는 사용자가 웹사이트 내 페이지를 더욱더 효율적으로 이동하게 하며, 사용자를 인식하고 환경설정을 유지하여 사용자가 어떻게 웹사이트를 이용하는지 이해하여 향후 웹사이트 방문 경험을 향상시킬 수 있도록 한다. (예: 필요한 정보를 더 쉽게 찾을 수 있게 함).

**Session 이란?**
세션이란  일정 시간동안  같은 사용자(정확하게 브라우저를 말한다)로 부터 들어오는 일련의 요구를 하나의 상태로 보고 그 상태를 일정하게 유지시키는 기술.  
또한 여기서  일정 시간이란 방문자가 웹 브라우저를 통해 웹 서버에 접속한 시점으로부터 웹 브라우저를 종료함으로써 연결을 끝내는 시점을 말하며 즉, 방문자가 웹서버에 접속해 있는 상태를 하나의 단위로 보고 세션이라고 칭한다는 것.

### [Cookie 와 Session의 차이 점]
**쿠키**의 경우는 방문자의 정보를  방문자 컴퓨터의 메모리에 저장하는 것을 말한다.
예를 들자면 ID나 비밀번호를 저장하거나 방문한 사이트를 저장하는데에 사용한다.
(인터넷 옵션에서 검색 기록 삭제할때 임시 파일, 열어본 페이지 목록, 쿠키, 저장된 암호 및 웹 양식 정보 삭제라고 되어있는것)

**세션**은 방문자의 요청에 따른 정보를 방문자 메모리에 저장하는 것이 아닌 **웹 서버가 세션 아이디 파일을 만들어 서비스가 돌아가고 있는  서버에 저장**을 하는것을 말한다.  

즉, 프로세스들 사이에서 통신을 하기 위해 메시지 교환을 통해 서로를 인식한 이후부터 **통신을 마칠 때까지의 기간동안 서버에 잠시 방문자 정보를 저장**한다는 것.

>그래서 **쿠키와 달리 세션은 사용자들의 로그인 정보에 대한 보안을 한층 업그레이드 할 수 있어 웹사이트에 방문하여 계속 접속을 유지할 때 이전의 접속 정보를 이용할 수 있는 방법**으로 많이들 사용하는 것이다.


## 2. Login 및 Logout 기능을 구현하여 실습 :pushpin:

**[Login 요구사항]**
* id , PassWord 하나라도 기입을 안하면 "아이디 및 비밀번호를 입력해주세요" 라는 문구출력
* Session객체의 생성 유무를 통해 이미로그인 중인지 확인하여 로그인에 성공 혹은 실패시 문구가 출력

**[Logout 요구사항]**
* 로그아웃 버튼 활성화
* 로그인 화면에서 로그아웃 버튼을 누르게 되면  Session객체의 생성 유무를 통해 로그인 상태이면 세션을 삭제시켜 다시 로그인을 할 수 있게 만들고, 로그인 상태가 아니라면 "로그인 상태가 아닙니다." 라는 문구가 뜨게 하기


**[HTML 코드]**

```java
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h3>로그인 화면</h3>
	<form action="LoginTest" method="POST">
	아이디 : <input type="text" name="id"><br/>
	비밀번호: <input type="password" name="pwd"><br/>
	<input type="submit" name="로그인"><br/>
	</form>
	<a href="LoginTest">로그아웃</a>
</body>
</html>
```
```java
<meta charset="UTF-8">
```
>문자를 UTF-8 형식으로 인코딩 하여 화면에 출력해주는 명령어이다.  

```java
<form action="LoginTest" method="POST">
```
> action에 들어가는 코드는 참조 및 연결시킬 Servlet 에노테이션명을 기입한다.
> method에 Get메서드 혹은 Post 메서드를 삽입하여 값을 삽입 할 것인지(Insert) 읽을것인지(Read) 나타낸다.

**[Servlet 코드]**
```java
package step02.session;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

@WebServlet("/LoginTest")
public class LoginLogoutServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public LoginLogoutServlet() {
		super();
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// 로그아웃 처리

		// 서버 응답시 클라이언트에게 메타정보 전달
		response.setContentType("text/html;charset=UTF-8");
		PrintWriter out = response.getWriter();
		HttpSession session = request.getSession();
		
		if(session != null && session.getAttribute("id") != null){
			// 세선의 정보삭제
			session.invalidate();
			out.print("로그아웃 완료");
		}else {
			out.print("로그인 상태가 아닙니다.");
		}

		out.close();
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		// 서버 응답시 클라이언트에게 메타정보 전달
		response.setContentType("text/html;charset=UTF-8");
		PrintWriter out = response.getWriter();

		// 클라이언트에서 입력한 id, pw 값 받기
		String id = request.getParameter("id");
		String pwd = request.getParameter("pwd");

		// id,pwd 둘 중 하나라도 입력 안하면 돌려보내기
		if (id.isEmpty() || pwd.isEmpty()) {
			out.printf("아이디 및 비밀번호를 입력해주세요");
			return;
		}

		// 세선객체생성
		HttpSession session = request.getSession();

		if (session.isNew() || session.getAttribute("id") == null) {
			session.setAttribute("id", id); // id 라는 이름의 키값으로 id값 저장
			out.print("로그인 완료.");
		} else {
			out.print("이미 로그인 상태입니다.");
		}
		out.close();
	}
}
```

```java
@WebServlet("/LoginTest")
```
> HTML 코드에서 호출하는 주소 생성

```java
	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		// 서버 응답시 클라이언트에게 메타정보 전달
		response.setContentType("text/html;charset=UTF-8");
		PrintWriter out = response.getWriter();

		// 클라이언트에서 입력한 id, pw 값 받기
		String id = request.getParameter("id");
		String pwd = request.getParameter("pwd");

		// id,pwd 둘 중 하나라도 입력 안하면 돌려보내기
		if (id.isEmpty() || pwd.isEmpty()) {
			out.printf("아이디 및 비밀번호를 입력해주세요");
			return;
		}

		// 세선객체생성
		HttpSession session = request.getSession();

		if (session.isNew() || session.getAttribute("id") == null) {
			session.setAttribute("id", id); // id 라는 이름의 키값으로 id값 저장
			out.print("로그인 완료.");
		} else {
			out.print("이미 로그인 상태입니다.");
		}
		out.close();
	}
```
>**로그인 메서드 구현**
>1. 문자형식 UTF-8로 변환  
>
>2. 화면에 출력이 되게 하는 PrintWriter  타입의 out 인스턴스 변수생성  
>
>3. 클라이언트에서 입력한 id,pw 값을 담는 변수 생성(getParameter의 반환값이 String 타입이기 때문에 변수의 타입도 동일하게 지정)  
>
>4. isEmpty 메서드는 객체의 값이 String타입으로 값이 하나라도 있으면 true 반환 없으면 false반환
>
>5. id 값과 pw값에  isEmpty 메서드를 사용하여 OR 로 비교하여 둘 중 하나라도 값이 없다면 "아이디 및 비밀번호를 입력해주세요"가 출력되도록 구현
>
>6. 로그인 상태유무를 확인하기 위해 세션 객체가 생성되어있는지로 확인하여 판별한다.
>
>7. session 객체에 isNew메서드를 사용하여 값이 있는지 없는지 확인하고 OR 연산자를 활용하여 getAttribute메서드 사용하여 id의 값이 널일 경우 if문 안쪽 실행
>
>8. session 객체에 setAttribute메서드를 사용하여 클라이언트가 입력한 아이디 값을 id 라는 이름의 키값으로 id값 저장
> 
> 9. 향후 세션에 해당 아이디로 로그인 시도시에는, 세션에 값이 이미 들어가 있기 때문에 if문 실패 코드가 출력된다.  

  
```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// 로그아웃 처리

		// 서버 응답시 클라이언트에게 메타정보 전달
		response.setContentType("text/html;charset=UTF-8");
		PrintWriter out = response.getWriter();
		HttpSession session = request.getSession();
		
		if(session != null && session.getAttribute("id") != null){
			// 세선의 정보삭제
			session.invalidate();
			out.print("로그아웃 완료");
		}else {
			out.print("로그인 상태가 아닙니다.");
		}

		out.close();
	}
```
>**로그아웃 메서드 구현**
>1. if 조건문 까지의 코드는 로그인 메서드와 동등하다. 단 OR 연산자에서 AND로 바뀌었다.
> 
> 2. 조건문이 일치하다면 invalidate() 메서드를 사용하여 해당 세선을 삭제시킨다.
>  
>  3. 조건문이 일치하지 않다면 "로그인 상태가 아닙니다." 라는 출력문이 나오도록 구현시킨다.
  







