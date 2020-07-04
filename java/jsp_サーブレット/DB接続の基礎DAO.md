<https://joytas.net/programming/jsp-servlet-db%e6%8e%a5%e7%b6%9a%e3%81%ae%e5%9f%ba%e7%a4%8edao>

MySQLでデータベース[lunchapp]を作成する。
データベースlunchappに[lunches]テーブルを作成する
初期データを挿入しておく

以下のリンクからjdbcをダウンロード(5.1.47)
<https://downloads.mysql.com/archives/c-j/>

WEB-INF/lib/の中にJDBC,META-INFの直下にcontext.xmlを配置する。
```xml
<?xml version="1.0" encoding="UTF-8" ?>
02
<Context>
03
  <Resource
04
      name="jdbc/jsp"
05
      auth="Container"
06
      type="javax.sql.DataSource"
07
      driverClassName="com.mysql.jdbc.Driver"
08
      url="jdbc:mysql://localhost:3306/lunchapp"
09
      connectionProperties="autoReconnect=true;verifyServerCertificate=false;useSSL=false;requireSSL=false;useUnicode=true;characterEncoding=UTF-8;"
10
      username="root"
11
      password="root"
12
      validationQuery="select 1"/>
13
 </Context>
```
modelパッケージにLunch.javaを作成する。
```java
package model;

import java.io.Serializable;

public class Lunch  implements Serializable{
	private int id;
	private String name;
	private String menu;
	public Lunch() {}
	public Lunch(String name,String menu) {
		this.name=name;
		this.menu=menu;
	}
	public Lunch(int id,String name,String menu) {
		this(name,menu);
		this.id=id;
	}
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getMenu() {
		return menu;
	}
	public void setMenu(String menu) {
		this.menu = menu;
	}

}
```
daoパッケージ内にLunchDAO.javaを作成する。
```java
package dao;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;

import javax.naming.Context;
import javax.naming.InitialContext;
import javax.naming.NamingException;
import javax.sql.DataSource;

import model.Lunch;

public class LunchDAO {
	private Connection db;
	private PreparedStatement ps;
	private ResultSet rs;

	//接続共通処理
	private void connect() throws NamingException, SQLException {
		Context context = new InitialContext();
		DataSource ds = (DataSource) context.lookup("java:comp/env/jdbc/jsp");
		this.db = ds.getConnection();
	}

	//切断共通処理
	private void disconnect() {
		try {
			if (rs != null) {
				rs.close();
			}
			if (ps != null) {
				ps.close();
			}
			if (db != null) {
				db.close();
			}
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}

	public List<Lunch> findAll() {
		List<Lunch> list = new ArrayList<>();
		try {
			this.connect();
			ps = db.prepareStatement("SELECT * FROM lunches");
			rs = ps.executeQuery();
			while (rs.next()) {
				int id = rs.getInt("id");
				String name = rs.getString("name");
				String menu = rs.getString("menu");
				Lunch l = new Lunch(id, name, menu);
				list.add(l);
			}
		} catch (NamingException | SQLException e) {

			e.printStackTrace();
		}finally {
			this.disconnect();
		}

		return list;
	}
	public void insertOne(Lunch lunch) {
		try {
			this.connect();
			ps=db.prepareStatement("INSERT INTO lunches(name,menu) VALUES(?,?)");
			ps.setString(1,lunch.getName());
			ps.setString(2,lunch.getMenu());
			ps.executeUpdate();
		} catch (NamingException | SQLException e) {
			e.printStackTrace();
		}finally {
			this.disconnect();
		}
	}
	public Lunch findOne(int id) {
		Lunch lunch=null;
		try {
			this.connect();
			ps=db.prepareStatement("SELECT * FROM lunches WHERE id=?");
			ps.setInt(1, id);
			rs=ps.executeQuery();
			if(rs.next()) {
				String name=rs.getString("name");
				String menu=rs.getString("menu");
				lunch=new Lunch(id,name,menu);
			}
		} catch (NamingException | SQLException e) {
			e.printStackTrace();
		}finally {
			this.disconnect();
		}

		return lunch;
	}
	public void updateOne(Lunch lunch) {
		try {
			this.connect();
			ps=db.prepareStatement("UPDATE lunches SET name=?,menu=? WHERE id=?");
			ps.setString(1, lunch.getName());
			ps.setString(2, lunch.getMenu());
			ps.setInt(3, lunch.getId());
			ps.executeUpdate();
		} catch (NamingException | SQLException e) {
			e.printStackTrace();
		}finally {
			this.disconnect();
		}
	}
	public void deleteOne(int id) {
		try {
			this.connect();
			ps=db.prepareStatement("DELETE FROM lunches WHERE id=?");
			ps.setInt(1, id);
			ps.executeUpdate();
		} catch (NamingException | SQLException e) {
			e.printStackTrace();
		}finally {
			this.disconnect();
		}
	}

}

```
controllerパッケージ内にRead.java(Servlet)を作成
```java
package controller;

import java.io.IOException;
import java.util.List;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import dao.LunchDAO;
import model.Lunch;

@WebServlet("/Read")
public class Read extends HttpServlet {
	private static final long serialVersionUID = 1L;

	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		LunchDAO dao=new LunchDAO();
		List<Lunch> list=dao.findAll();
		request.setAttribute("list", list);
		RequestDispatcher rd=request.getRequestDispatcher("/WEB-INF/view/read.jsp");
		rd.forward(request, response);
	}

}
```
/WEB-INF/viewフォルダにread.jspを作成
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" import="model.*,java.util.*"%>
<%
List<Lunch> list=(List<Lunch>)request.getAttribute("list");
%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<a href="/lunchapp/Create">新規追加</a>
<%if(list !=null && list.size()>0){ %>
<table border="1">
<tr><th>id</th><th>name</th><th>menu</th><th></th></tr>
<%for(Lunch lunch:list){ %>
<tr>
<td><%=lunch.getId() %></td>
<td><%=lunch.getName() %></td>
<td><%=lunch.getMenu() %></td>
<td>
<a href="/lunchapp/Update?id=<%=lunch.getId() %>">更新</a>
<a href="/lunchapp/Delete?id=<%=lunch.getId() %>" onclick="return confirm('id=<%=lunch.getId()%>を削除してよろしいですか？');">削除</a>
</td>
</tr>
<%} %>
</table>
<%} %>
</body>
</html>
```
controllerパッケージ内にCreate.java(Servlet)を作成
```java
package controller;

import java.io.IOException;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import dao.LunchDAO;
import model.Lunch;

/**
 * Servlet implementation class Create
 */
@WebServlet("/Create")
public class Create extends HttpServlet {
	private static final long serialVersionUID = 1L;

  
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		RequestDispatcher rd=request.getRequestDispatcher("/WEB-INF/view/create.jsp");
		rd.forward(request, response);
	}


	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		request.setCharacterEncoding("UTF-8");
		String name=request.getParameter("name");
		String menu=request.getParameter("menu");
		Lunch lunch=new Lunch(name,menu);
		LunchDAO ld=new LunchDAO();
		ld.insertOne(lunch);

		response.sendRedirect("/lunchapp/Read");
	}

}
```
/WEB-INF/viewフォルダにcreate.jspを作成
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<form action="/lunchapp/Create" method="post">
なまえ:<input type="text" name="name"><br>
メニュー:<input type="text" name="menu"><br>
<button type="submit">追加</button>
</form>
</body>
</html>
```
controllerパッケージ内にUpdate.java(Servlet)を作成
```java
package controller;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import dao.LunchDAO;
import model.Lunch;

/**
 * Servlet implementation class Update
 */
@WebServlet("/Update")
public class Update extends HttpServlet {
	private static final long serialVersionUID = 1L;


	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		String s_id=request.getParameter("id");
		if(s_id==null) {
			response.sendRedirect("/lunchapp/Read");
		}else {
			LunchDAO dao=new LunchDAO();
			Lunch lunch=dao.findOne(Integer.parseInt(s_id));
			request.setAttribute("lunch", lunch);
			request.getRequestDispatcher("/WEB-INF/view/update.jsp").forward(request, response);
		}
	}

	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		request.setCharacterEncoding("UTF-8");
		String id=request.getParameter("id");
		String name=request.getParameter("name");
		String menu=request.getParameter("menu");
		Lunch lunch=new Lunch(Integer.parseInt(id),name,menu);
		LunchDAO dao=new LunchDAO();
		dao.updateOne(lunch);
		response.sendRedirect("/lunchapp/Read");
	}

}
```
/WEB-INF/viewフォルダにupdate.jspを作成
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" import="model.*,java.util.*"%>
<%
Lunch lunch=(Lunch)request.getAttribute("lunch");
%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<form action="/lunchapp/Update" method="Post">
なまえ:<input type="text" name="name" value="<%=lunch.getName()%>"><br>
メニュー:<input type="text" name="menu" value="<%=lunch.getMenu() %>"><br>
<input type="hidden" name="id" value="<%=lunch.getId() %>">
<button type="submit">更新</button>
</form>
</body>
</html>
```
controllerパッケージ内にDelete.java(Servlet)を作成
```java
package controller;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import dao.LunchDAO;

/**
 * Servlet implementation class Delete
 */
@WebServlet("/Delete")
public class Delete extends HttpServlet {
	private static final long serialVersionUID = 1L;


	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		String id=request.getParameter("id");
		if(id !=null) {
			LunchDAO dao=new LunchDAO();
			dao.deleteOne(Integer.parseInt(id));
		}
		response.sendRedirect("/lunchapp/Read");
	}



}
```
