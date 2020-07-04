<%=変数名%> → 変数に代入されている値

<%=演算式%> → 演算結果

<%=オブジェクト.メソッド()%> → メソッドの戻り値

<%=オブジェクト%> → オブジェクト.toString()の戻り値

<%-- ... --%> コメント
***
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" import="ex.Employee"%>
    <%
    Employee emp=new Employee("0001","湊 雄輔");
    %>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<%for(int i=0;i<10;i++){ %>
	<%if((i+1)%3==1){ %>
		<p style="color:red;">IDは<%=emp.getId() %>、名前は<%=emp.getName() %>です</p>
	<%}else{ %>
	<p>IDは<%=emp.getId() %>、名前は<%=emp.getName() %>です</p>
	<%} %>
<%} %>
</body>
</html>
