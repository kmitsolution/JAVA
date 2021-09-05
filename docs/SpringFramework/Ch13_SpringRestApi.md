# Create a Rest Api service using Spring boot

<b>Step1:-></b> Create a spring Maven Web project ( Goto https://start.spring.io/  and Add Spring Web dependcies).<br />
Group:- com.kmit.springboot.restapi <br />
Artifact: - restservice <br />
Name:- restservice <br />
Package name:- com.kmit.springboot.restapi.restservice <br />

<b>Step2:-></b> Import the project in Eclipse (File-->import-->Existing Maven Project and refer the Extracted folder ) <br />
<b>Step 3:-> Create below classes <br />

  Employee.java
  ```java
  package com.kmit.springboot.restapi.restservice;

public class Employee {
private int Id;
private String name;
private int sal;
public void setId(int id) {
	Id = id;
}
public void setName(String name) {
	this.name = name;
}
public void setSal(int sal) {
	this.sal = sal;
}
public int getId() {
	return Id;
}
public String getName() {
	return name;
}
public int getSal() {
	return sal;
}
public Employee(int id, String name, int sal) {
	super();
	Id = id;
	this.name = name;
	this.sal = sal;
}


@Override
public String toString() {
	return "Employee [Id=" + Id + ", name=" + name + ", sal=" + sal + "]";
}
}

  ```
  
  EmployeeController.java
```java
  package com.kmit.springboot.restapi.restservice;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.Arrays;
import java.util.List;

@RestController
public class EmployeeController {
@GetMapping("/list")
 public List<Employee> getEmps(){
	return Arrays.asList( new Employee(1,"Raman",5));
}
}

```  

<b>Step 3:-></b>  Run the application and visit the url http://localhost:8080/list and it should return a json object as below <br />
  [{"name":"Raman","sal":5,"id":1}]
