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

