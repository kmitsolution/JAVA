# XML configurations into Spring Boot

<b>Step 1</b> Create an XML file(springprop.xml) under src/main/resources (Create movie class as public class not abstract)
```java
public  class Movies {
	 public void watch() { System.out.println("Movies");}
}

```
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans-2.5.xsd">

 <bean id="moviesxml" 
       class="com.kmit.spring.FirstProject.Movies">
 </bean>  
<bean id="videolibxml" class="com.kmit.spring.FirstProject.VideoLibrary">
    <property name="movies" ref="moviesxml"></property>
  </bean>

 

  <!-- more bean definitions go here -->

</beans>
```

<b>Step 2</b> Load the Context with the help of XML Path

```java
@SpringBootApplication

public class FirstProjectApplication {

	public static void main(String[] args) {

		ClassPathXmlApplicationContext run= 
				new ClassPathXmlApplicationContext("springprop.xml");

		VideoLibrary v=run.getBean(VideoLibrary.class);
		v.InCinema();
	}

}

```
<b>Step 3</b> Run the application
