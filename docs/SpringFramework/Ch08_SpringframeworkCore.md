# Spring Core
Spring enables you to build applications from "plain old Java objects" (POJOs) and to apply enterprise services non-invasively to POJOs. This capability applies to the Java SE programming model and to full and partial Java EE.

<b>Note:-</b> So far we are using Spring Boot framework.Now let's see how Spring Core framework works without Spring Boot.

## Convert Spring Boot to Spring Core

<b>Step 1 </b> Remove Spring Boot dependency from pom.xml (Shown as below). <br />
 ```xml
 <dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter</artifactId>
 </dependency>
 ```
 <b> Step 2 </b> Add Spring Core dependency (Shown as below). <br />
 ```xml
 <dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-core</artifactId>
 </dependency>
 <dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-context</artifactId>
 </dependency>
        
```
<b> Step 3 </b> Remove @SpringBootApplication from your main class ( in our examples it is FirstProjectApplication ). <br />
<b> Step 4 </b> Add @Configuration,@ComponentScan("") annotation to your main class <br />
<b> Step 5 </b> remove the below code from your main class 
```java
ApplicationContext run =
				SpringApplication.run(FirstProjectApplication.class, args);
```
<b> Step 6 </b> Add below code to your main class (FirstProjectApplication)
```java
ApplicationContext run= 
				new AnnotationConfigApplicationContext(FirstProjectApplication.class);
```

### Here is full code to follow
```java
@Configuration
@ComponentScan("")
public class FirstProjectApplication {

	public static void main(String[] args) {
	/* ApplicationContext can load bean definitions, wire beans together
	 * , and dispense beans upon request
	 */
		/* you can use this code also with ApplicationContext but it gives a warning on run variable we can solve this using run.close() but close() is available with AnnotationConfigApplicationContext class.
    ApplicationContext run= 
				new AnnotationConfigApplicationContext(FirstProjectApplication.class);
	 */
			AnnotationConfigApplicationContext run= 
				new AnnotationConfigApplicationContext(FirstProjectApplication.class);

		VideoLibrary v=run.getBean(VideoLibrary.class);
		v.InCinema();
		run.close();
	}

}
```
<b> Step 7 </b> Run the application.






