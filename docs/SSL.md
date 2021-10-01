## Create Spring boot RESTful service with https

### Step 1:- Create Spring Boot App
1. Create a spring boot app using https://start.spring.io/
2. Add Web Dependency

### Step 2:- Add Settings for SSL in application.properties file
```xml
server.port=8443
server.ssl.key-alias=https-example
server.ssl.key-store-type=JKS
server.ssl.key-password=changeit
server.ssl.key-store=classpath:https-example.jks
```

### Step 3:- Create key value pair SSL file and copy it to resources folder
1. keytool -genkey -alias https-example -storetype JKS -keyalg RSA -keysize 2048 -validity 365 -keystore https-example.jks
2. keytool -importkeystore -srckeystore https-example.jks -destkeystore https-example.jks -deststoretype pkcs12  
3. copy https-example.jks C:\Projects\Java8\Microservices\ssl\src\main\resources\

### Step 4:- Create some code
```java
package com.https.ssl;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/hello")
public class HelloController {

	@GetMapping
	public String Hello() {
		return "Hello World";
	}
}

```
