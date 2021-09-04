# @Component
  To create a class level annotation 
# @Primary
When there are multiple beans available of same type in Spring container, all of them are qualified to be autowired to single-valued dependency. That causes ambiguity and leads to throw an exception by framework. @Primary indicates that a bean should be given preference when multiple candidates are qualified to autowire a single-valued dependency.

There should be only one @Primary bean among same type of beans.
```java
// Movies.java
package com.kmit.spring.FirstProject;

public abstract class Movies {
	 abstract void watch();
}

```
```java
// BollywoodMovies.java (A bean class)
package com.kmit.spring.FirstProject;

import org.springframework.context.annotation.Primary;
import org.springframework.stereotype.Component;

@Component
@Primary
public class BollywoodMovies extends Movies {

	@Override
    void watch() {
      System.out.println("Watching Bollywood Movie");

    }

}
```

```java
// HollywoodMovies.java class 
package com.kmit.spring.FirstProject;

import org.springframework.stereotype.Component;

@Component
public class HollywoodMovies extends Movies {

    @Override
    void watch() {
      System.out.println("Watching Hollywood Movie");

    }

}
```

```java
//VideoLibrary.class (Bean class and has dependency on Movies class [autowired])
package com.kmit.spring.FirstProject;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class VideoLibrary {
	@Autowired
	Movies movies; 
    public VideoLibrary(Movies watchmovie) { //Created a parameterized constructor for loosely couple and called Constructor Autowiring
        movies = watchmovie;
          }
   	  
        
    public void InCinema() {
        movies.watch();
          }
}
```
 <b> Note:-</b> We can remove constructor and either use the setter method or even if we are not using the setter method, framework automatically makes property as Dependent property  

```java
//FirstProjectApplication.java class  (main class to implement)
package com.kmit.spring.FirstProject;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;
import org.springframework.context.ConfigurableApplicationContext;

@SpringBootApplication
public class FirstProjectApplication {

	public static void main(String[] args) {
	/* ApplicationContext can load bean definitions, wire beans together
	 * , and dispense beans upon request
	 */
		ApplicationContext run =
				SpringApplication.run(FirstProjectApplication.class, args);
		VideoLibrary v=run.getBean(VideoLibrary.class);
		v.InCinema();
	}

}

```
## @Qualifier Annotation
By using the @Qualifier annotation, we can eliminate the issue of which bean needs to be injected. By including the @Qualifier annotation, together with the name of the specific implementation we want to use

```java
package com.kmit.spring.FirstProject;

import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.context.annotation.Primary;
import org.springframework.stereotype.Component;

@Component
@Qualifier("bollywood")
public class BollywoodMovies extends Movies {

	@Override
    void watch() {
      System.out.println("Watching Bollywood Movie");

    }

}
```

```java
package com.kmit.spring.FirstProject;

import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.context.annotation.Primary;
import org.springframework.stereotype.Component;

@Component
@Qualifier("hollywood")
public class HollywoodMovies extends Movies {

    @Override
    void watch() {
      System.out.println("Watching Hollywood Movie");

    }

}
```
### To inject in VideoLibrary class using @Qualifier
```java
package com.kmit.spring.FirstProject;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.stereotype.Component;

@Component
public class VideoLibrary {
	@Autowired
	@Qualifier("hollywood")
	Movies movies; 
 
    public void InCinema() {
        movies.watch();
          }

	public void setMovies(Movies movies) {
		this.movies = movies;
	}
}
```
### Call using Application Context
```java
package com.kmit.spring.FirstProject;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;
import org.springframework.context.ConfigurableApplicationContext;

@SpringBootApplication
public class FirstProjectApplication {

	public static void main(String[] args) {
	/* ApplicationContext can load bean definitions, wire beans together
	 * , and dispense beans upon request
	 */
		ApplicationContext run =
				SpringApplication.run(FirstProjectApplication.class, args);
		VideoLibrary v=run.getBean(VideoLibrary.class);
		v.InCinema();
	}

}

```
