## Spring Boot Actuator
Spring Boot includes a number of additional features to help you monitor and manage your application when you push it to production. You can choose to manage and monitor your application by using HTTP endpoints or with JMX. Auditing, health, and metrics gathering can also be automatically applied to your application.

### Step 1:- Create a Spring Boot application 
1. Create a spring boot project (Group name:-> com.actuator, Artifact ID:->actuator-example Packagename:-> com.learn)
2. Add Dependency of Spring Web and MySql
3. Generate the project.
4. Import Maven project in eclipse.
5. Acutator URL:-  https://docs.spring.io/spring-boot/docs/current/reference/html/actuator.html

### Step 2:- Add a Controller (Home.Controller)
1. Create a class HomeController under learn.com package
```java
package com.learn;

import java.util.HashMap;
import java.util.Map;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HomeController {

	@GetMapping("/get-data")
	public Map<String,String> get(){
		 Map<String,String> map=new HashMap<String,String>();  
		  map.put("Name","Amit");  
		return map;
	}
}

```
2. Run the application at localhost:8080/get-data
3. You will get the json output with {"Name":"Amit"}

### Step 3:- Create a Bean class and Autowired with Controller
1. Create a Bean class - Called Student
```java
package com.learn;

import org.springframework.stereotype.Component;

@Component
public class Student {

}

```
2. Autowired with Controller class
```java
@RestController
public class HomeController {

	@Autowired
	private Student student;
	
	@GetMapping("/get-data")
	public Map<String,String> get(){
		 Map<String,String> map=new HashMap<String,String>();  
		  map.put("Name","Amit");  
		return map;
	}
}
```
### Step 4:- Add Actuator dependency in pom.xml
1.
```xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
```

2. Run the application 
3. you will find the new end point called /actuator
4. http://localhost:8081/actuator on browser (Check the port number)
5. You can check the health of the actuator/health

### Step 5:- Expose End Points 
1. You can expose the end points which we can expose on actuator web site (like beans,http etc)
2. Add management.endpoints.web.exposure.include=* in application.properties file (You can mention specified endpoints instead of * and You can use exclude to exclude beans)
3. save the project and run
4. Check the log of spring boot you will find now around 13 end points are exposed.
5. http://localhost:8081/actuator/  open in the browser and you will find that there are some set of end points has been exposed.
6. In Mapping Endpoint you can find your GetMapping method get-data

### Step 6:- Show health details and configure actuator url
1. Add the below code in applicaiton.properties file

management.endpoints.web.exposure.include=* <br />
management.endpoint.health.show-details=always < br/>
management.endpoints.web.base-path=/admin <br />

2. save and run the application.
3. check /admin/health   and you will get the detailed health information.

### Step 7:- Create Custom Health information
1. Create your own class for Health check
```java
package com.learn;

import org.springframework.boot.actuate.health.Health;
import org.springframework.boot.actuate.health.HealthIndicator;
import org.springframework.stereotype.Controller;

@Controller
public class MyDbHealthService implements HealthIndicator {

	public boolean IsHealthy() {
		return true;
	}
	@Override
	public Health health() {
		// TODO Auto-generated method stub
		if (IsHealthy()) {
			return Health.up().withDetail("Database", "UP").build();
		}
		return Health.up().withDetail("Database", "Down").build();
	}

}
```

2.
