

### Step1 
Create a Spring Boot project with Spring Initializer and add Web Dependency
### Step2 Create a Contact class
```java
package com.java.restful.webservice.restwebservice;

public class Contact {
private String id;
private String name;
public Contact(String id, String name) {
	super();
	this.id = id;
	this.name = name;
}
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
}

```

# Step 3 Add a AddressbookResouce class
```java
package com.java.restful.webservice.restwebservice;

import java.util.ArrayList;
import java.util.concurrent.ConcurrentHashMap;
import java.util.concurrent.ConcurrentMap;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;

import antlr.collections.List;

@RestController
public class AddressBookResource {
	ConcurrentMap<String,Contact> contacts = new ConcurrentHashMap<String, Contact>() ;
    @GetMapping("/{id}")
	public Contact getContact(@PathVariable String id) {
		return contacts.get(id);
	}
    @GetMapping("/")
	public ArrayList<Contact> getAllContacts(){
    	return new ArrayList<Contact>(contacts.values());
		
	}
    @PostMapping("/")
	public Contact addContact(@RequestBody Contact contact) {
		contacts.put(contact.getId(),contact);
		return contact;
	}
}

```
## Step 4 Run the project in PostMan
1. Run the Get Request http://localhost:8080
2. Run Post Request by providing the body like { "id": "1", "name": "Raman"}

## Step 5 Add Swagger Dependency

```xml
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger2</artifactId>
    <version>2.9.2</version>
</dependency>
```

## Step 6 Enable Swagger2 Application

```java
@SpringBootApplication
@EnableSwagger2
public class RestwebserviceApplication {

	public static void main(String[] args) {
		SpringApplication.run(RestwebserviceApplication.class, args);
	}

}

```

## Step 7 Restart the applicaton
1. visit http://localhost:8080/v2/api-docs you will find lot of documentation of your API

## Step 8 Add Swagger UI dependency.

```xml
<!-- https://mvnrepository.com/artifact/io.springfox/springfox-swagger-ui -->
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger-ui</artifactId>
    <version>2.9.2</version>
</dependency>
```

## Step 9 Add /api Mapping to AddressbookResource class

```java
@RestController
@RequestMapping("/api")
public class AddressBookResource {

```

## Step 10 Run below url
http://localhost:8080/swagger-ui.html
