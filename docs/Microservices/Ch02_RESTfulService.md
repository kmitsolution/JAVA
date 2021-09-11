# RESTful WebService
RESTful web services are built to work best on the Web. Representational State Transfer (REST) is an architectural style that specifies constraints, such as the uniform interface, that if applied to a web service induce desirable properties, such as performance, scalability, and modifiability, that enable services to work best on the Web. In the REST architectural style, data and functionality are considered resources and are accessed using Uniform Resource Identifiers (URIs), typically links on the Web.

### Resource
<ul>
  <li> A resource has an URI(uniform resource identifier) like /emp/salaries/1 or /emp/salaries</li>
  <li> POST :- Create Operation eg POST/emps </li>
  <li> GET :- GET Operations eg GET/emps or GET/emps/1</li>
  <li> DELETE:- Delete Operation DELETE/emps/1</li>
  <li> PUT :- Update Operations PUT/emps/1 </li>
  <li> A resource can have XML,JSON,HTML representation</li>
</ul>  

# Creating RESTful service using Spring Boot
 
### Step1 :- Initialize Spring Boot project
<ul>
  <li>Open https://start.spring.io/ </li>
  <li>Create a Maven project with latest Release version(2.54)</li>
  <li>Add Dependencies ( Web and Spring DevOps Tools,JPA,H2 Database) </li>
  <li>Generate the project (Java 11 or java 8)</li>
  <li> Extract the downloaded zip file </li>
  <li> Open this project in Eclipse IDE (File-->Import) </li>
  <li> Check pom.xml and you will observe that all the depenencies has been added. </li>
  <li> Open java file under src/main/java and Run the applicaiton as a java Application </li>
  <li> Because it is new project but you will be able to see log enties under console output </li>
</ul>

### Step2 :- Create a Basic REST Service
<ul>
  <li>Create a class called HelloWorld under same package</li>
  <li>Add below code </li>
  </ul>
  
  ```java
  package com.java.restful.webservice.restwebservice;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloWorld {
	
	//GET service
	//Return Hello World
	//URI- /helloworld
	@RequestMapping(method= RequestMethod.GET,path="/hello-world")
	public String helloworld() {
		return "Hello World";
	}

}
```     
<ul>
<li> Run this application and check http://localhost:8080/hello-world </li>  
</ul>  

### Step3 :- Use @GetMapping Annotation
Replace <b>@RequestMapping</b> with <b>@GetMapping</b> and check the output it should be same

```java
@RestController
public class HelloWorld {
	
	//GET service
	//Return Hello World
	//URI- /helloworld
	@GetMapping(path="/hello-world")
	public String helloworld() {
		return "Hello World";
	}

}
```

### Step4 :- use @GetMapping to return a Bean class

#### Create a class Called HelloWorldBean

```java
package com.java.restful.webservice.restwebservice;

public class HelloWorldBean {

	private String message;

	@Override
	public String toString() {
		return "HelloWorldBean [message=" + message + "]";
	}

	public String getMessage() {
		return message;
	}

	public void setMessage(String message) {
		this.message = message;
	}

	public HelloWorldBean(String message) {
		// TODO Auto-generated constructor stub
		this.message=message;
	}

}
```

```java
package com.java.restful.webservice.restwebservice;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloWorld {
	
	//GET service
	//Return Hello World
	//URI- /helloworld
	@GetMapping(path="/hello-world")
	public String helloworld() {
		return "Hello World";
	}
    @GetMapping(path="/hello-world-bean")
    public HelloWorldBean helloworldbean() {
    	return new HelloWorldBean("Hello World Bean");
    }
}
```
#### Run the application and you will get output in json format

{"message":"Hello World Bean"}


