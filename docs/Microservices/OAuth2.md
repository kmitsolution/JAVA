## OAuth

OAuth 2.0 is an authorization protocol and NOT an authentication protocol. As such, it is designed primarily as a means of granting access to a set of resources, for example, remote APIs or user's data. OAuth 2.0 uses Access Tokens.

1. Add Oauth2 dependency in your springboot api

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-oauth2-client</artifactId>
    </dependency>
```

2. Check your applicaiton it should ask for the Form level Authentication.
3. Create a Github app (Settings -->Developer Settings ---> Github App and Get Client ID and Secret key)
4. callback value is http://localhost:9000/login/oauth2/code/github
5. In application properties file add below lines
```

spring.security.oauth2.client.registration.github.clientId =  
spring.security.oauth2.client.registration.github.clientSecret= 

```

5. Run the application.
