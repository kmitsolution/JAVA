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
  <li>Generate the project (Java 11 or java 8) I am creating with package com.java.restful.webservice.restwebservice</li>
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

### Step 5 :- Understandand internal working of this project

1. Add <b>logging.level.org.springframework = debug</b>   in application.properties file. <br/>
2. Run the application and Copy the logs into a Notepad file and lets observe that.  <br/>
3. Search text CONDITIONS EVALUATION REPORT in the file.  <br/>
4. In pom.xml file we have added a dependency <br/>
```xml
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```
Hence the log indicates that a DispatcherServlet AutoConfiguration is found
<b>DispatcherServletAutoConfiguration matched:</b>

Also it configures the Error Configuration

<b>ErrorMvcAutoConfiguration matched: </b> <br />
<b>ErrorMvcAutoConfiguration#basicErrorController matched:</b> <br />
<b>ErrorMvcAutoConfiguration#errorAttributes matched:</b> <br />
<b>ErrorMvcAutoConfiguration.DefaultErrorViewResolverConfiguration#conventionErrorViewResolver matched: </b> <br />
<b>ErrorMvcAutoConfiguration.WhitelabelErrorViewConfiguration matched:</b> <br />
<b>HttpEncodingAutoConfiguration matched:</b> These methods are responsible to convert Bean to Json <br />
<b>JacksonAutoConfiguration matched:</b> these configuration converts json to bean and bean to json.<br />
<b>Mapping Servlet: </b> There is dispatcherServlet (FronController) to [/]. dispatcherServlet detects all Get,Put etc mapping.dispatcherServlet sends the response using @ResponseBody of @RestController (JacksonAutoConfiguration).

### Step 6 :- Path Variable (@PathVariable)
If you want to pass the parameter to service request then we use path variables eg /hello-world/name  so name is path variable
```java
  //URI - /hello-world/raman
    @GetMapping(path="/hello-world/{name}")
    public HelloWorldBean helloworldbeanPathVariable(@PathVariable String name) {
    	return new HelloWorldBean(String.format("Name=%s", name));
    }
```
<b>Output </b><br/>
{"message":"Name=raman"}


### Step 7 :- Create User Bean and User Service
Create a User class and UserDaoService class

```java
package com.java.restful.webservice.restwebservice.user;

import java.util.Date;

public class User {

	private Integer id;
	private String name;
	private Date birthDate;
	
	protected User() {
		// TODO Auto-generated constructor stub
	}
	
	public User(Integer id, String name, Date birthDate) {
		super();
		this.id = id;
		this.name = name;
		this.birthDate = birthDate;
	}
	public Integer getId() {
		return id;
	}
	public void setId(Integer id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public Date getBirthDate() {
		return birthDate;
	}
	public void setBirthDate(Date birthDate) {
		this.birthDate = birthDate;
	}
	@Override
	public String toString() {
		return "User [id=" + id + ", name=" + name + ", birthDate=" + birthDate + "]";
	}
	
}

```

```java
package com.java.restful.webservice.restwebservice.user;

import java.util.ArrayList;
import java.util.Date;
import java.util.List;

import org.springframework.stereotype.Component;



@Component
public class UserDaoService {

	private static List<User> users = new ArrayList<>();

	private static int usersCount = 3;

	static {
		users.add(new User(1, "Raman", new Date()));
		users.add(new User(2, "Manoj", new Date()));
		users.add(new User(3, "Raj", new Date()));
	}

	public List<User> findAll() {
		return users;
	}

	public User save(User user) {
		if (user.getId() == null) {
			user.setId(++usersCount);
		}
		users.add(user);
		return user;
	}

	public User findOne(int id) {
		for (User user : users) {
			if (user.getId() == id) {
				return user;
			}
		}
		return null;
	}
}

```

```java
package com.java.restful.webservice.restwebservice.user;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class UserResource {

	@Autowired
	private UserDaoService service;

	@GetMapping("/users")
	public List<User> retrieveAllUsers() {
		return service.findAll();
	}

	@GetMapping("/users/{id}")
	public User retrieveUser(@PathVariable int id) {
		return service.findOne(id);
	}

}
```
<b> Run the application </b> http://localhost:8080/users      

#### Output will be
```json
[{"id":1,"name":"Raman","birthDate":"2021-09-12T09:48:11.221+00:00"},{"id":2,"name":"Manoj","birthDate":"2021-09-12T09:48:11.221+00:00"},{"id":3,"name":"Raj","birthDate":"2021-09-12T09:48:11.221+00:00"}]
```
http://localhost:8080/users/1

```json
{"id":1,"name":"Raman","birthDate":"2021-09-12T09:48:11.221+00:00"}
```
<b> Note: -> </b> Check the inspect on browser for http://localhost:8080/users and check the Network Element and You can see the response Body and Status code.

### Step 8:- Implementing POST Method (To create user)

Add @PostMapping to UserResource class
```java
@PostMapping("/users")
public void createUser(@RequestBody User user) {
	User saveduser=service.save(user);
	}
```
<b>Rest API Client</b> I am using Postman for POST Method (http://localhost:8080/user) and Add below body

```json
{"name":"Rohit","birthDate":"2021-09-12T09:48:11.221+00:00"}
```

### Run Get/users method and you should be able to newly created record.

### Step 9:- Return Status code(201) and Userid(Check header's location) from the POST Request.

```java
import java.net.URI;

@PostMapping("/users")
	public ResponseEntity<Object> createUser(@RequestBody User user) {
		User saveduser=service.save(user);
		 URI location = ServletUriComponentsBuilder
				.fromCurrentRequest()
				.path("{id}")
				.buildAndExpand(saveduser.getId()).toUri();
		return ResponseEntity.created(location).build();
	}
```	

### Step 10:- Exception Handling using GET Method

Update the below code for GET method.

```java
package com.java.restful.webservice.restwebservice.user;

public class UserNotFoundException extends RuntimeException {

	public UserNotFoundException(String message) {
		// TODO Auto-generated constructor stub
		super(message);
	}

}
```
```java
@GetMapping("/users/{id}")
	public User retrieveUser(@PathVariable int id) {
		User user = service.findOne(id);
		if (user==null)
			throw new UserNotFoundException("id-" + id);
		return user;
	}
```

<b> Run GET Request for a user which does not exist and You will recieve 500 internal error </b></br>
Now lets make it more meaningful error message, make below changes (Add @ResponseStatus(HttpStatus.NOT_FOUND)) to UserNotFoundException and Now You will return 404 Error and also check message and path, it should return id which we are searching.

```java
@ResponseStatus(HttpStatus.NOT_FOUND)
public class UserNotFoundException extends RuntimeException {

	public UserNotFoundException(String message) {
		// TODO Auto-generated constructor stub
		super(message);
	}

}
```

### Step 10 Create a Generic Exeception

Create a Generic Exception class

```java
package com.java.restful.webservice.restwebservice.exception;

import java.util.Date;

public class ExceptionResponse {

	private Date timestamp;
	private String message;
	private String details;
	public ExceptionResponse(Date timestamp, String message, String details) {
		super();
		this.timestamp = timestamp;
		this.message = message;
		this.details = details;
	}
	public Date getTimestamp() {
		return timestamp;
	}
	public void setTimestamp(Date timestamp) {
		this.timestamp = timestamp;
	}
	public String getMessage() {
		return message;
	}
	public void setMessage(String message) {
		this.message = message;
	}
	public String getDetails() {
		return details;
	}
	public void setDetails(String details) {
		this.details = details;
	}
	
}

```

```java
package com.java.restful.webservice.restwebservice.exception;

import java.util.Date;

import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.context.request.WebRequest;
import org.springframework.web.servlet.mvc.method.annotation.ResponseEntityExceptionHandler;

import com.java.restful.webservice.restwebservice.user.UserNotFoundException;

@ControllerAdvice //Global Exception Handling 
@RestController
public class GenericException extends ResponseEntityExceptionHandler{
	
	//It is for all Exception
	@ExceptionHandler(Exception.class)
	public final ResponseEntity<Object> handleAllExceptions(Exception ex,WebRequest request)
	{
		ExceptionResponse exceptionResponse = new ExceptionResponse(new Date(),
				ex.getMessage(),
				request.getDescription(false));
		
		return new ResponseEntity(exceptionResponse,HttpStatus.INTERNAL_SERVER_ERROR);
		
	}

	//It is more specific to USER Class Exception
	@ExceptionHandler(UserNotFoundException.class)
	public final ResponseEntity<Object> handleUserNotFoundException(UserNotFoundException ex,WebRequest request)
	{
		ExceptionResponse exceptionResponse = new ExceptionResponse(new Date(),
				ex.getMessage(),
				request.getDescription(false));
		
		return new ResponseEntity(exceptionResponse,HttpStatus.NOT_FOUND);
		
	}
}


```

<b>Now Run the API with GET Method like localhost:8080/users/500 it should return customized error message.</b>

### Step 11 :- Implement Delete Method

Modify UserDaoService by adding deleteById method

```java
package com.java.restful.webservice.restwebservice.user;

import java.util.ArrayList;
import java.util.Date;
import java.util.Iterator;
import java.util.List;

import org.springframework.stereotype.Component;



@Component
public class UserDaoService {

	private static List<User> users = new ArrayList<>();

	private static int usersCount = 3;

	static {
		users.add(new User(1, "Raman", new Date()));
		users.add(new User(2, "Manoj", new Date()));
		users.add(new User(3, "Raj", new Date()));
	}


	public User save(User user) {
		if (user.getId() == null) {
			user.setId(++usersCount);
		}
		users.add(user);
		return user;
	}

	
	public List<User> findAll() {
		// TODO Auto-generated method stub
		return users;
	}

	public User findOne(int id) {
		// TODO Auto-generated method stub
		for (User user : users) {
			if (user.getId() == id) {
				return user;
			}
		}
		return null;
	}
	
	public User deleteById(int id) {
		// TODO Auto-generated method stub
		Iterator<User> iterator =users.iterator();
		while (iterator.hasNext())
		 {
			User user=iterator.next();
			if (user.getId() == id) {
				iterator.remove();
				return user;
			}
		}
		return null;
	}
}

```

<b> Add @DeleteMapping</b>

```java
package com.java.restful.webservice.restwebservice.user;


import java.net.URI;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.servlet.support.ServletUriComponentsBuilder;






@RestController
public class UserResource {

	@Autowired
	private UserDaoService service;

	@GetMapping("/users")
	public List<User> retrieveAllUsers() {
		return service.findAll();
	}

	@GetMapping("/users/{id}")
	public User retrieveUser(@PathVariable int id) {
		User user = service.findOne(id);
		if (user==null)
			throw new UserNotFoundException("id-" + id);
		return user;
	}
	@PostMapping("/users")
	public ResponseEntity<Object> createUser(@RequestBody User user) {
		User saveduser=service.save(user);
		 URI location = ServletUriComponentsBuilder
				.fromCurrentRequest()
				.path("{id}")
				.buildAndExpand(saveduser.getId()).toUri();
		return ResponseEntity.created(location).build();
	}
	
	@DeleteMapping("/users/{id}")
	public void deleteUser(@PathVariable int id) {
		User user = service.deleteById(id);
		if (user==null)
			throw new UserNotFoundException("id-" + id);
		
	}

}
```

<b>Check DELETE Method in Postman and it should delete the existing id and if no id found then it should throw the exception </b>

### Step 12: Adding Validation Dependency

Add below entry in pom.xml
``` xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```
	




