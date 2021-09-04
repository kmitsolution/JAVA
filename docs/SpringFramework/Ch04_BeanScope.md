## Bean Scope
When we define the bean then you have an option to declare the scope of the bean. Below are the supportive bean scopes
<ul>
  <li><b>singleton (default) :-</b> This scopes the bean definition to a single instance per Spring IoC container</li>
  <li><b>prototype :-</b> This scopes a single bean definition to have any number of object instances. </li>
  <li><b>request :-</b> This scopes a bean definition to an HTTP request. Only valid in the context of a web-aware Spring ApplicationContext.</li>
  <li><b>session :-</b> This scopes a bean definition to an HTTP session. Only valid in the context of a web-aware Spring ApplicationContext. </li>
</ul>

### Example of Singleton scope
In this example I am reating 2 variables v and v1 and both will return the same bean object with same hash code. You can use the scope annotation @Scope(ConfigurableBeanFactory.SCOPE_SINGLETON) for singleton scope. <br />
The output will be similar to below
    //com.kmit.spring.FirstProject.VideoLibrary@3b0f7d9d
    //com.kmit.spring.FirstProject.VideoLibrary@3b0f7d9d

```java
@SpringBootApplication
public class FirstProjectApplication {

	public static void main(String[] args) {
	/* ApplicationContext can load bean definitions, wire beans together
	 * , and dispense beans upon request
	 */
		ApplicationContext run =
				SpringApplication.run(FirstProjectApplication.class, args);
		
    VideoLibrary v=run.getBean(VideoLibrary.class);  
		VideoLibrary v1=run.getBean(VideoLibrary.class);
 
		System.out.println(v1);
		System.out.println(v);
		v.InCinema();
	}

}
```

### Example of prototype scope
 In the VideoLibrary class add annotation @Scope("prototype") or @Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE).
```java
@Component
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
public class VideoLibrary {
	@Autowired
    @Qualifier("holly")
	Movies movies; 
    /*public VideoLibrary(Movies watchmovie) { //Created a parameterized constructor for loosely couple
        movies = watchmovie;
          }
      */  
    public void InCinema() {
        movies.watch();
          }

	public void setMovies(Movies movies) {
		this.movies = movies;
	}
}

```
#### Note
I am reating 2 variables v and v1 and both will return the same bean object with different hash code.<br />
The output will be similar to below
    //com.kmit.spring.FirstProject.VideoLibrary@59b07d9d
    //com.kmit.spring.FirstProject.VideoLibrary@3b0f7d9d
```java
@SpringBootApplication
public class FirstProjectApplication {

	public static void main(String[] args) {
	/* ApplicationContext can load bean definitions, wire beans together
	 * , and dispense beans upon request
	 */
		ApplicationContext run =
				SpringApplication.run(FirstProjectApplication.class, args);
		
    VideoLibrary v=run.getBean(VideoLibrary.class);  
		VideoLibrary v1=run.getBean(VideoLibrary.class);
 
		System.out.println(v1);
		System.out.println(v);
		v.InCinema();
	}

}
```

## Scope for Dependency classes.
For example the dependency class Hollywoodmovies is of @Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE) and class VideoLibrary has @Scope(ConfigurableBeanFactory.SCOPE_SINGLETON) and if you use below code then it returns the same hash code for movies objects

```java
    VideoLibrary v=run.getBean(VideoLibrary.class);
		VideoLibrary v1=run.getBean(VideoLibrary.class);
		Movies m=v.movies;
		Movies m1=v1.movies;
		System.out.println(v1);
		System.out.println(v);
		System.out.println(m1);
		System.out.println(m);
```

<b> To Create a different bean object for the Dependency then use ScopedProxyMode.TARGET_CLASS

 ```java
@Component
@Qualifier("holly")
@Scope(value=ConfigurableBeanFactory.SCOPE_PROTOTYPE,
             proxyMode=ScopedProxyMode.TARGET_CLASS)
public class HollywoodMovies extends Movies {

    @Override
    void watch() {
      System.out.println("Watching Hollywood Movie");

    }

}
 ``` 
