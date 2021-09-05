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
		System.out.println(run.getBeanDefinitionCount()); // it should show 2 beans
		System.out.println(run.getBeanDefinitionNames()); // display beans which get loaded VideoLibrary and Movies
		VideoLibrary v=run.getBean(VideoLibrary.class);
		v.InCinema();
	}

}

```
<b>Step 3</b> Run the application

### If You need to display all the beans which are defined in XML or defined using Spring (@Component) 

<b>Step1</b> Create a XML Context (Create a new xml file springcontext.xml)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	   xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans-2.5.xsd
		   http://www.springframework.org/schema/context
           http://www.springframework.org/schema/context/spring-context-2.5.xsd	
			">
			
<context:component-scan base-package="com.kmit.spring.FirstProject" />
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
				new ClassPathXmlApplicationContext("springcontext.xml");
		System.out.println(run.getBeanDefinitionCount()); // it should count all the beans
		System.out.println(run.getBeanDefinitionNames()); // display all the beans in base package
		VideoLibrary v=run.getBean(VideoLibrary.class);
		v.InCinema();
	}

}

```

