
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
