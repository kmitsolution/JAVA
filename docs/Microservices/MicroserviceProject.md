# Microservice Project

### Step 1:- Create a  spring boot project with Web Dependecies
1. Create a Spring boot application using https://start.spring.io/
2. Add Web dependency
3. Generate the project

### Step 2:- Create a user class and Contacts class 

```java
package com.user.entity;

public class Contact {

	private Long cId;
	private String email;
	private String contactName;
	private Long userId;
	public Contact(Long cId, String email, String contactName, Long userId) {
		super();
		this.cId = cId;
		this.email = email;
		this.contactName = contactName;
		this.userId = userId;
	}
	public Contact() {
		super();
		// TODO Auto-generated constructor stub
	}
	public void setcId(Long cId) {
		this.cId = cId;
	}
	public void setEmail(String email) {
		this.email = email;
	}
	public void setContactName(String contactName) {
		this.contactName = contactName;
	}
	public void setUserId(Long userId) {
		this.userId = userId;
	}
	
}

```

```java
package com.user.entity;

import java.util.ArrayList;
import java.util.List;

package com.user.entity;


import java.util.ArrayList;
import java.util.List;

public class User {
	private Long userid;
	private String name;
	private String phone;
	
	List<Contact> contacts = new ArrayList<>();

	public User(Long userid, String name, String phone, List<Contact> contacts) {
		super();
		this.userid = userid;
		this.name = name;
		this.phone = phone;
		this.contacts = contacts;
	}

	public User(Long userid, String name, String phone) {
		super();
		this.userid = userid;
		this.name = name;
		this.phone = phone;
	}

	public User() {
		super();
	}

	public void setUserid(Long userid) {
		this.userid = userid;
	}

	public void setName(String name) {
		this.name = name;
	}

	public Long getUserid() {
		return userid;
	}

	public String getName() {
		return name;
	}

	public String getPhone() {
		return phone;
	}

	public List<Contact> getContacts() {
		return contacts;
	}

	public void setPhone(String phone) {
		this.phone = phone;
	}

	public void setContacts(List<Contact> contacts) {
		this.contacts = contacts;
	}
	

}

```

## Step3 Create user service

```java
package com.user.service;

import com.user.entity.User;

public interface UserService {

	public User getUser(Long Id);
}

```

## Step 4 Create user service implementation

```java
package com.user.service;

import java.util.ArrayList;
import java.util.List;

import org.springframework.stereotype.Service;

import com.user.entity.User;
@Service
public class UserServiceImpl implements UserService{

	ArrayList<User> lists = new ArrayList<>();
	
	public UserServiceImpl() {
		super();
		lists.add(new User(111L, "Raman", "12345"));
		lists.add(new User(112L, "Manoj", "123456"));
		lists.add(new User(113L, "Rahul", "1234567"));
		// TODO Auto-generated constructor stub
	}


	@Override
	public User getUser(Long Id) {
		// TODO Auto-generated method stub.
		//return null;
		return this.lists.stream().filter( user -> user.getUserid().equals(Id)).findAny().orElse(null);
	}
	
}

```

### Step 5 Add Controller

```java
package com.user.controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.user.entity.User;
import com.user.service.UserService;

@RestController
@RequestMapping("/user")
public class UserController {

	@Autowired
	private UserService userservice;
	@GetMapping("/{userid}")
	public User getUser(@PathVariable("userid") Long userid) {
		return this.userservice.getUser(userid);
	}
}
```

# Lets Create 2nd Microservice for Contact

1. https://start.spring.io/
2. Add Web dependency
3. Groupid:- com.contact
4. Artifact id: contact_service
5. Packagename :- com.contact

### Step 6 Add Contact class

```java
package com.user.entity;

public class Contact {

	private Long cId;
	private String email;
	private String contactName;
	private Long userId;
	public Contact(Long cId, String email, String contactName, Long userId) {
		super();
		this.cId = cId;
		this.email = email;
		this.contactName = contactName;
		this.userId = userId;
	}
	public Contact() {
		super();
		// TODO Auto-generated constructor stub
	}
	public void setcId(Long cId) {
		this.cId = cId;
	}
	public void setEmail(String email) {
		this.email = email;
	}
	public void setContactName(String contactName) {
		this.contactName = contactName;
	}
	public void setUserId(Long userId) {
		this.userId = userId;
	}
	
}

```

### Step 7 Add ContactService Interface

```java
package com.contact.service;

import java.util.List;

import com.user.entity.Contact;

public interface ContactService {

	public List<Contact> getCotnactsofUser(Long userId);
}

```

### Step 8 Add Service Implementation class

```java
package com.contact.service;

import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;

import com.user.entity.Contact;

@Service
public class ContactServiceImpl implements ContactService {

	List<Contact> list= new ArrayList();
	public ContactServiceImpl() {
		super();
		list.add(new Contact(1L,"raman@gmail.com","Raman",111L));
		list.add(new Contact(1L,"raj@gmail.com","Raj",112L));
		list.add(new Contact(1L,"Manoj@gmail.com","Manoj",113L));
		list.add(new Contact(1L,"kunal@gmail.com","Kunal",114L));
		// TODO Auto-generated constructor stub
	}

	@Override
	public List<Contact> getCotnactsofUser(Long userId) {
		// TODO Auto-generated method stub
		return this.list.stream().filter( contact -> contact.getUserid().equals(Id)).collect(Collectors.toList());
	}

}
```

### Add Contact Controller
```java
package com.contact.controller;

import java.util.List;

import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.contact.service.ContactService;
import com.user.entity.Contact;

@RestController
@RequestMapping("/contact")
public class ContactController {
	
	@Autowired
	private ContactService contactservice;
	
	@RequestMapping("/user/{userId}")
	public List<Contact> getContacts(@PathVariable("userId") Long userId){
	   return this.contactservice.getCotnactsofUser(userId);	
	}
}

```


## Now we need that these 2 services should communicate to each other.

### Step 8 Add @Bean and RestTemplate to UserApplication

```java
public class UserServiceApplication {

	public static void main(String[] args) {
		SpringApplication.run(UserServiceApplication.class, args);
	}

	@Bean
	public RestTemplate restTemplate() {
		return new RestTemplate();
	}
}

```

### Step 9 Change UserController to add RestTemplate to communicate between 2 services

```java
package com.user.controller;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.client.RestTemplate;

import com.user.entity.User;
import com.user.service.UserService;

@RestController
@RequestMapping("/user")
public class UserController {

	@Autowired
	private UserService userservice;
	
	@Autowired
	private RestTemplate restTemplate;
	@GetMapping("/{userid}")
	public User getUser(@PathVariable("userid") Long userid) {
		//return this.userservice.getUser(userid);
		User user=this.userservice.getUser(userid);
		
		List contacts= this.restTemplate.getForObject("http://localhost:9002/contact/user/" + userid, List.class);
		user.setContacts(contacts);
		return user;
	}
}

```

### Step 10 Run User Application

1. http://localhost:8080/user/111
2. You will be able to find the contact details also with above url


### Eureka Server for Service Discovery

1. Create a spring boot project with Eureka Server Dependency 
2. Open the project in Eclipse
3. Add in the application.properties file
```
eureka.client.registerWithEureka = false
eureka.client.fetchRegistry = false
server.port = 8761
```
OR YOU CAN CREATE YAML FILE (application.yml)

```
eureka:
   client:
      registerWithEureka: false
      fetchRegistry: false
server:
   port: 8761
```

4. Enable the Eureka Server
```java
package com.eserver;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;

@SpringBootApplication
@EnableEurekaServer
public class EserverApplication {

	public static void main(String[] args) {
		SpringApplication.run(EserverApplication.class, args);
	}

}

```

6. Run the application
7. visit http://localhost:8761/
8. It should show the Eureka Server Interface
9. Goto your user service project and Contact Service project and Add below dependecies of Eureka's clien
```xml
<properties>
    <java.version>1.8</java.version>
    <spring-cloud.version>2020.0.4</spring-cloud.version>
  </properties>
  <dependencies>
    <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
    </dependency>

    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-test</artifactId>
      <scope>test</scope>
    </dependency>
  </dependencies>
  <dependencyManagement>
    <dependencies>
      <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-dependencies</artifactId>
        <version>${spring-cloud.version}</version>
        <type>pom</type>
        <scope>import</scope>
      </dependency>
    </dependencies>
  </dependencyManagement>

```
10. Change in application.properties files to add the service name

```
spring.application.name=user-service
```
11. Make similar changes in contact service
12. In user-service replace "http://localhost:9002/contact/user/ with "http://contact-service/contact/user/
13. In user application add @LoadBalanced Annotation
```java
package com.user;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.client.loadbalancer.LoadBalanced;
import org.springframework.context.annotation.Bean;
import org.springframework.web.client.RestTemplate;

@SpringBootApplication
public class UserServiceApplication {

	public static void main(String[] args) {
		SpringApplication.run(UserServiceApplication.class, args);
	}

	@Bean
	@LoadBalanced
	public RestTemplate restTemplate() {
		return new RestTemplate();
	}
}
```

14. Check http://localhost:8080/user/111 , you should be able to see the result.


### API GATEWAY

1. Create a Spring Boot project 
2. add Dependency spring Routing Gateway,Eureka Discovery Client, Acutator
3. Generate the project
4. Open in Eclipse
5. Enable Eureka Client
```java
package com.apiGateway;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.EnableEurekaClient;

@SpringBootApplication
@EnableEurekaClient
public class ApigatewayApplication {

	public static void main(String[] args) {
		SpringApplication.run(ApigatewayApplication.class, args);
	}

}
```
6. Add in application properties
```
server.port=8999

spring.application.name=ApiGateway

spring.cloud.gateway.discovery.locator.lower-case-service-id=true
spring.cloud.gateway.routes[0].id=user-service
spring.cloud.gateway.routes[0].uri=lb://user-service
spring.cloud.gateway.routes[0].predicates[0]=Path=/user/**

spring.cloud.gateway.routes[1].id=contact-service
spring.cloud.gateway.routes[1].uri=lb://contact-service
spring.cloud.gateway.routes[1].predicates[0]=Path=/contact/user/**


```
7. Run the application on port number 8999 http://localhost:8999/user/111
8. You should get invoke the service
