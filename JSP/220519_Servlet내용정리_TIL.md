# 22.05.19 Servlet 수업 내용정리:pencil2:
## 1. 페이지 이동 :pushpin:

### Redirct
간단히 말하면 최초의 request를 유지하지 않고 클라이언트에서 request가 발생했을때 새로운 request를 생성해 사용하는 것이며 Redirect는 지속성이아닌 일회성이 강하다.

예를들어, 내가 회원가입을 완료하고 띄워지는 화면이 로그인이 되어있는 화면이었으면 좋겟으나 로그인을 해야하는 화면이 띄워진다면 그것은 Redirect방식을 사용하여 내가 다시 입력한 정보를 요청하여 로그인해야한다.

**[ 간단한예시]**
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<form action="otherSite">
		<input type="radio" name="site" value="naver" />네이버<br /> <input
			type="radio" name="site" value="google" />구글<br /> <input
			type="submit" value="이동" />
	</form>
</body>
</html>
```
> html 파일에서 네이버 혹은 구글을 선택하는 라디오를 생성하고
> submit타입의 이동 버튼을 누르게 되면, 해당 플랫폼의 주소로 넘어가는 틀을 구현하였다.
---
```java
package step03.pagemove;

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/otherSite")
public class RedirectServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		
		// radio tag에 입력된 값 받기
		String site = request.getParameter("site");
		// 그 값이 naver면 naver.com로 이동, google이면 google.com으로 이동
		if(site.equals("naver")) {
			// naver.com으로 요청 재지정(redirect)
			response.sendRedirect("http://www.naver.com");
		} else if(site.equals("google")) {
			// google.com
			response.sendRedirect("http://www.google.com");
		}
	}

}
```
> radio의 value 값을 비교하여 만약 선택된 value값이 naver라면 naver의 주소로 이동하라는 sendRedirect 메서드를 사용하여 response를 받고 선택된 value값이 google 이라면 google의 주소값으로 이동하라는 구문을 작성하였다.
>   
>   만약 naver의 주소값의 응답을 받았다면 해당  URL은 네이버의 주소로 변경될 것이다. 이게바로 Redirct 방식이다. 
---

### Forward

포워드는 간단히 말하면 최초의 request를 계속 유지하며 페이지를 이동하는 방식이다.

포워드는 requset가 이루어지면 해당 request는 일회성이아닌 지속성을 가지게 되며 request내에 담긴 정보들이 웹페이지를 이동하면서 계속 사용되는 것이다.

예로 들어, 내가 회원가입을 완료하고 웹페이지가 넘어갈때 출력되는 화면이 자동적으로 로그인이 되어있는 화면이라면 이것은 회원가입 정보를 기입하고 완료버튼을 눌렀을때 생긴 request가 다음페이지 요청시에도 유지되어 그안에 담긴 정보들을 활용해 나온 결과가 되는 것이다.

**[ 간단한예시]**

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<form action="mouseInsert" method="post">
	이름 : <input type="text" name="name"/><br/>
	국적 : <input type="text" name="country"/><br/>
	주소 : <input type="text" name="address"/><br/>
	<input type="submit" value="등록"/><br/>
	
	
	</form>
</body>
</html>
```
>html 파일에서 mouse의  이름 국적 주소를 입력하는 text 형식의 input태그를 삽입하였다. 등록을 하면 다음페이지에서는 등록한 데이터에 대해서 값을 나타내주는 작업을 하려 한다.
---
```java
package step03.pagemove;

public class Mouse {
	private String name;
	private String country;
	private String address;
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getCountry() {
		return country;
	}
	public void setCountry(String country) {
		this.country = country;
	}
	public String getAddress() {
		return address;
	}
	public void setAddress(String address) {
		this.address = address;
	}
}

```
> mouse에 대한 설계를 한다. 멤버변수를 private으로 설정하고
> 외부에서 값을 설정 및 가져오기 위해 getter / setter 메서드를 활용했다.
---
```java
// MouseServlet1.java
package step03.pagemove;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/mouseInsert")
public class MouseServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html;charset=UTF-8");
		PrintWriter out = response.getWriter();
		
		request.setCharacterEncoding("UTF-8");
		
		// form에서 입력된 값 받기
		String name = request.getParameter("name");
		String country = request.getParameter("country");
		String address = request.getParameter("address");
		
		Mouse mouse = new Mouse();
		mouse.setName(name);
		mouse.setCountry(country);
		mouse.setAddress(address);
		System.out.println("DB 등록 처리 진행");
		
		request.setAttribute("mouse", mouse); // "mouse"라는 이름의 key값으로 mouse 인스턴스를 담았음.
		
		RequestDispatcher rd = request.getRequestDispatcher("mouseResult");
		
		// 실제 포워딩
		rd.forward(request, response);
		
		out.close();
	}

}
```
> 클라이언트가 입력한 데이터를 등록하기 위해 doPost 메서드를 사용한다.
> form에서 입력한 값을 담는 변수를 생성하여 입력값을 저장한다
> mouse 인스턴스를 생성하여  setter 메서드를 활용하여 이름을 설정해준다.
> setAttribute 메서드를 활용하여 "mouse"라는 이름의 key값으로 mouse 인스턴스를 담았다.

**여기서 잠깐**
```java
		RequestDispatcher rd = request.getRequestDispatcher("mouseResult");
		
		// 실제 포워딩
		rd.forward(request, response);
```
이 부분에 RequestDispatcher 타입, 그리고 getRequestDispatcher 메서드에 대해 아무리 공부하여도 무슨 메서드 인지, 어떤 목적으로 사용되는지 의문점으로 남아있다. 이부분은 내일 강사님께 질문드려야 겠다.


