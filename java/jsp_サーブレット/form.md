```
<input type="hidden" name="名前" value="値">
<a href="リクエスト先?名前=値>...</a>
<form action="リクエスト先?名前=値" method="post">...</form>
```
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<form action="/formLesson/FormSampleServlet" method="post">
名前:<input type="text" name="name"><br>
性別:
男<input type="radio" name="gender" value="0">
女<input type="radio" name="gender" value="1"><br>
<input type="submit" value="送信">
</form>
</body>
</html>
```




****
```java
import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Servlet implementation class FormSampleServlet
 */
@WebServlet("/FormSampleServlet")
public class FormSampleServlet extends HttpServlet {

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		request.setCharacterEncoding("UTF-8");
		String name=request.getParameter("name");
		String gender=request.getParameter("gender");
		response.setContentType("text/html; charset=utf-8");
		PrintWriter out=response.getWriter();
		//System.out.printf("送信データname:%s,gender:%s%n", name,gender);
		out.println("<!DOCTYPE html>");
		out.println("<html>");
		out.println("<head>");
		out.println("<meta charset='utf-8' />");
		out.println("<title>Lesson</title>");
		out.println("</head>");
		out.println("<body>");
		out.println("<p>こんにちは"+name+"さん！</p>");
		out.println("</body>");
		out.println("</html>");
	}

}

