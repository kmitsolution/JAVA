## @PostConstruct
When we annotate a method in Spring Bean with @PostConstruct annotation, it gets executed after the spring bean is initialized. We can have only one method annotated with @PostConstruct annotation. This annotation is part of Common Annotations API and it's part of JDK module javax.

## @PreDestroy
When we annotate a Spring Bean method with PreDestroy annotation, it gets called when bean instance is getting removed from the context. This is a very important point to understand – if your spring bean scope is “prototype” then it’s not completely managed by the spring container and PreDestroy method won’t get called.

```java
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
    @PostConstruct 
    public void init() {
    	System.out.println("Constructor is called");
     }
    
    @PreDestroy
    public void shutdown() {
    	System.out.println("Destructor is called");
    }
}

```
