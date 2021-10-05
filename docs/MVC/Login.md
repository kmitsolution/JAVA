1. Created a web maven project
2. Edited index.jsp

```html
<!DOCTYPE html>
<html>
<head>
<html>
<body>
<%
response.sendRedirect(request.getContextPath() + "/login");
%>
</body>
</html>

```
3. in web.xml

```
<servlet>
        <servlet-name>login</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <load-on-startup>1</load-on-startup>
    </servlet>

    <servlet-mapping>
        <servlet-name>login</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
   ``` 
   
   4. Add depenedencies in pom.xml
   
   ```xml
<dependency>
		<groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>4.3.13.RELEASE</version>
    </dependency>
    <dependency>
		<groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>4.3.13.RELEASE</version>
    </dependency>
    <dependency>
		<groupId>javax.servlet</groupId>
        <artifactId>jstl</artifactId>
        <version>1.2</version>
    </dependency>
   ```
   
   5. create a file login-servlet.xml under WEB-INF folder
   
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd"
        >
    <context:component-scan base-package="com.login"></context:component-scan>
    <mvc:annotation-driven enable-matrix-variables="true"/>
     <mvc:default-servlet-handler/>
    <bean id="viewResolver"
    class="org.springframework.web.servlet.view.InternalResourceViewResolver">
      <property name="prefix" value="/WEB-INF/jsp/"/>
    <property name="suffix" value=""/>
    
</bean>

</beans>
```

6. Add a login.jsp in WEB-INF/jsp/ folder
7. Add below html in login.jsp page

```html
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Login Page</title>
</head>
<script>
function myFunction() {
  var uname=document.getElementById("uname").value;
  var pass=document.getElementById("pass").value;
  //alert(uname.length);
  if( uname.length==0)
	  {
	  alert("user name cannot be blank");
	  return false;
	  }
  if( pass.length==0)
  {
  alert("password cannot be blank");
  return false;
  }

}
</script>
</head>
<body>
<form action="access">
 Username : <input type="text" id="uname" name="uname" > <br />
 Password : <input type="password" id="pass" name="pass" > <br />
 
 <input type="submit" value="Signin" onclick="myFunction()">
 </form>
</body>
</html>
```

8. Add a package com.login and add a class called loginController.java

```java
package com.login;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.servlet.ModelAndView;

@Controller
public class loginController {
	
	@RequestMapping("/login")
	public String hello() {
		return "login.jsp";
	}


	
	@RequestMapping("/access")
	public ModelAndView access(HttpServletRequest request, HttpServletResponse response)
	{
		ModelAndView mv =new ModelAndView();
		mv.setViewName("access.jsp");
		String result;
		String uname=request.getParameter("uname");
		String pass=request.getParameter("pass");
		if(uname.equals("Spring") && pass.equals("Boot"))
			result="Welcome to Spring Boot Project";
		else
			result="Access Denied";
		mv.addObject("result",result);
		return mv;
	}
	
}

```
10. Create access.jsp page under WEB-INF/Jsp

```html
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1" isELIgnored="false"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Authentication Page</title>
</head>
<body>
Permission =<%= request.getAttribute("result") %>
Permission = ${result}
</body>
</html>
```

11. Run the application 

12. Add JSLT dependency which is required for accessing the data to jsp. 

 ```
    	<dependency>
	    <groupId>jstl</groupId>
	    <artifactId>jstl</artifactId>
	    <version>1.2</version>
	</dependency>
	```
13. Add JSLT core ui tag in home.jsp

```
  <%@ taglib uri = "http://java.sun.com/jsp/jstl/core" prefix = "c" %>  
	<%@page isELIgnored="false" %>  

	In the content section lets extract value of name attribute

	<c:out value = "${ result }"/>
```

```java
package com.login;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.servlet.ModelAndView;

@Controller
public class loginController {

	@RequestMapping("/login")
	public String loginpage()
	{
		return "loginpage.jsp";
	}
	
	@RequestMapping("/access")
	public ModelAndView login(HttpServletRequest request, HttpServletResponse response) {
		String uname= request.getParameter("user");
		String pass= request.getParameter("pass");
		ModelAndView mv = new ModelAndView();
		mv.setViewName("access.jsp");
		if ( uname.equals("raman") && pass.equals("raja"))
		{
			mv.addObject("result","ok");
		}
		else
			mv.addObject("result","Access Denied");
		return mv;
	}
	
	  @RequestMapping("/home")
	    public String Home( Model m) //added Model 
		{
			
	    	String str="home";
	    	//Adding the attribute name and use name attribute in jsp page
	    	// JSLT dependency is required for this
	    	m.addAttribute("page",str); 
	    	return "home.jsp";
		}
	  @RequestMapping("/main")
	    public String Main1( Model m) //added Model 
		{
			
	    	String str="Main";
	    	//Adding the attribute name and use name attribute in jsp page
	    	// JSLT dependency is required for this
	    	m.addAttribute("page",str); 
	    	return "home.jsp";
		}
	   
}

```

```html
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<%@ taglib uri = "http://java.sun.com/jsp/jstl/core" prefix = "c" %>  
	<%@page isELIgnored="false" %>      
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Home</title>
</head>
<body>
<c:out value = "${ page }"/>

<div class="col-md-10">
         <c:if test="${page=='home' }">
            <h1>This is home page</h1>
          </c:if>
          <c:if test="${page=='add' }">
            <h1>This is add page</h1>
          </c:if>
       </div>
<form action="intro">
<input type=submit value=intro >       	
</body>

<form action="main">
<input type=submit value=main >
</form>

</html>
```


### BootStrap with Jsp
```java
package com.login;

public class Test {
public Test(String id, String name) {
		super();
		this.id = id;
		this.name = name;
	}
private String id;
private String name;
public void setId(String id) {
	this.id = id;
}
public void setName(String name) {
	this.name = name;
}
public String getId() {
	return id;
}
public String getName() {
	return name;
}
@Override
public String toString() {
	return "Test [id=" + id + ", name=" + name + "]";
}
public Test() {
	super();
	// TODO Auto-generated constructor stub
}
}

```
```java
package com.login;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.servlet.ModelAndView;

@Controller
public class loginController {

	@RequestMapping("/login")
	public String loginpage()
	{
		return "loginpage.jsp";
	}
	
	@RequestMapping("/access")
	public ModelAndView login(HttpServletRequest request, HttpServletResponse response) {
		String uname= request.getParameter("user");
		String pass= request.getParameter("pass");
		ModelAndView mv = new ModelAndView();
		mv.setViewName("access.jsp");
		if ( uname.equals("raman") && pass.equals("raja"))
		{
			mv.addObject("result","ok");
		}
		else
			mv.addObject("result","Access Denied");
		return mv;
	}
	
	  @RequestMapping("/home")
	    public String Home( Model m) //added Model 
		{
			
	    	String str="home";
	    	//Adding the attribute name and use name attribute in jsp page
	    	// JSLT dependency is required for this
	    	m.addAttribute("page",str); 
	    	return "home.jsp";
		}
	  @RequestMapping("/main")
	    public String Main1( Model m) //added Model 
		{
			
	    	String str="Main";
	    	//Adding the attribute name and use name attribute in jsp page
	    	// JSLT dependency is required for this
	    	m.addAttribute("page",str); 
	    	return "main.jsp";
		}
	  @RequestMapping("/intro")
	    public String intro( Model m) //added Model 
		{
			
	    	String str="Main";
	    	//Adding the attribute name and use name attribute in jsp page
	    	// JSLT dependency is required for this
	    	m.addAttribute("page",str); 
	    	return "intro.jsp";
		}
	   
}

```

```html
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<%@ taglib uri = "http://java.sun.com/jsp/jstl/core" prefix = "c" %>  
	<%@page isELIgnored="false" %>      
	
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-F3w7mX95PdgyTmZZMECAngseQB83DfGTowi0iMjiWaeVhAn4FJkqJByhZMI3AhiU" crossorigin="anonymous">

    <title>Home</title>
  </head>
  <body>
    <div class="container mt-3">
    <h1>Customer Form</h1>
   <div class="row mt-4">
    <div class="col-md-2">
       <h3 class="text-center">Menu</h3>
       <div class="list-group">
		  <button type="button" class="list-group-item list-group-item-action active" aria-current="true">
		    Home
		  </button>
		  <button type="button" class="list-group-item list-group-item-action">
		  <a href='<c:url value='/intro'></c:url>' >
		    Intro
		  </a>
		  </button>
		  <button type="button" class="list-group-item list-group-item-action">
		  <a href='<c:url value='/main'></c:url>' >
		    Main
		  </a>
		  </button>
		  </div>
    </div>
    <div class="col-md-10">
     <c:if test="${ page =='home' }">
       <h1 class="text-center">Home Page</h1>
      </c:if>
      <c:if test="${ page =='intro' }">
       <h1 class="text-center">Intro Page</h1>
      </c:if>
      <c:if test="${ page =='main' }">
       <h1 class="text-center">Main Page</h1>
      </c:if> 
    </div>
    </div>
    </div>

    
    
    
    
    
    
    <!-- Optional JavaScript; choose one of the two! -->

    <!-- Option 1: Bootstrap Bundle with Popper -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.1/dist/js/bootstrap.bundle.min.js" integrity="sha384-/bQdsTh/da6pkI1MST/rWKFNjaCP5gBSY4sEBT38Q/9RBh9AH40zEOg7Hlq2THRZ" crossorigin="anonymous"></script>

    <!-- Option 2: Separate Popper and Bootstrap JS -->
    <!--
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.3/dist/umd/popper.min.js" integrity="sha384-W8fXfP3gkOKtndU4JGtKDvXbO53Wy8SZCQHczT5FMiiqmQfUpWbYdTil/SxwZgAN" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.1/dist/js/bootstrap.min.js" integrity="sha384-skAcpIdS7UcVUC05LJ9Dxay8AXcDYfBJqt1CJ85S/CFujBsIzCIv+l9liuYLaMQ/" crossorigin="anonymous"></script>
    -->
  </body>
</html>
```

### ModelAttribute

```html
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
    <%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %>  
<!DOCTYPE html>  
    
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-F3w7mX95PdgyTmZZMECAngseQB83DfGTowi0iMjiWaeVhAn4FJkqJByhZMI3AhiU" crossorigin="anonymous">

    <title>Home</title>
  </head>
  <body>
  
  


<form:form action="save" method="post" modelAttribute="test">
<div class="form-group">
<form:input path="id" cssClass="form-control" />

</div>  
             
<div class="form-group">
<form:input path="name" cssClass="form-control" />

</div>  
<div><input type="submit" /></div>
</form:form>
    

    
    
    
    
    
    
    <!-- Optional JavaScript; choose one of the two! -->

    <!-- Option 1: Bootstrap Bundle with Popper -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.1/dist/js/bootstrap.bundle.min.js" integrity="sha384-/bQdsTh/da6pkI1MST/rWKFNjaCP5gBSY4sEBT38Q/9RBh9AH40zEOg7Hlq2THRZ" crossorigin="anonymous"></script>

    <!-- Option 2: Separate Popper and Bootstrap JS -->
    <!--
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.3/dist/umd/popper.min.js" integrity="sha384-W8fXfP3gkOKtndU4JGtKDvXbO53Wy8SZCQHczT5FMiiqmQfUpWbYdTil/SxwZgAN" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.1/dist/js/bootstrap.min.js" integrity="sha384-skAcpIdS7UcVUC05LJ9Dxay8AXcDYfBJqt1CJ85S/CFujBsIzCIv+l9liuYLaMQ/" crossorigin="anonymous"></script>
    -->
  </body>
</html>
```

```java
package com.login;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.servlet.ModelAndView;

@Controller
public class loginController {

	@RequestMapping("/login")
	public String loginpage()
	{
		return "loginpage.jsp";
	}
	
	@RequestMapping("/access")
	public ModelAndView login(HttpServletRequest request, HttpServletResponse response) {
		String uname= request.getParameter("user");
		String pass= request.getParameter("pass");
		ModelAndView mv = new ModelAndView();
		mv.setViewName("access.jsp");
		if ( uname.equals("raman") && pass.equals("raja"))
		{
			mv.addObject("result","ok");
		}
		else
			mv.addObject("result","Access Denied");
		return mv;
	}
	
	  @RequestMapping("/home")
	    public String Home( Model m) //added Model 
		{
			
	    	String str="home";
	    	//Adding the attribute name and use name attribute in jsp page
	    	// JSLT dependency is required for this
	    	m.addAttribute("page",str); 
	    	return "home.jsp";
		}
	  @RequestMapping("/add")
	    public String Main1( Model m) //added Model 
		{
			
	    	String str="add";
	    	//Adding the attribute name and use name attribute in jsp page
	    	// JSLT dependency is required for this
	    	Test t = new Test();
	    	m.addAttribute("page",str);
	    	m.addAttribute("test",t);
	    	
	    	
	    	return "main.jsp";
		}
	  @RequestMapping("/intro")
	    public String intro( Model m) //added Model 
		{
			
	    	String str="Main";
	    	//Adding the attribute name and use name attribute in jsp page
	    	// JSLT dependency is required for this
	    	m.addAttribute("page",str); 
	    	return "intro.jsp";
		}
	  @RequestMapping(value="/save",method=RequestMethod.POST)
	    public String save(@ModelAttribute("test") Test t, Model m) //added Model 
		{
		  System.out.println(t);
			return "home.jsp";
	    	
		}
	   
}

```
