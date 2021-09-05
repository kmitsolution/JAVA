# Read External Property file

<b>Step1:-</b> Create a property file call app.prop in src/main/resources folder and add below entry <br />
moviename=DDLJ <br />
<b>Step2:-</b> Use @Value Annotation for read value from external property file  <br />
```java
@Component
public class VideoLibrary {
	@Autowired
	Movies movies; 
    /*public VideoLibrary(Movies watchmovie) { //Created a parameterized constructor for loosely couple
        movies = watchmovie;
          }
      */  
	@Value("${moviename}")
	private String moviename1;
    public void InCinema() {
        movies.watch();
        System.out.println(moviename1);
          }
	public Movies getMovies() {
		return movies;
	}
	public void setMovies(Movies movies) {
		this.movies = movies;
  }
}
```

<b>Step 3:-</b> Refer the filename in main class <br />
```java
@SpringBootApplication
@PropertySource("classpath:app.prop")
public class FirstProjectApplication {

	public static void main(String[] args) {
	/* ApplicationContext can load bean definitions, wire beans together
	 * , and dispense beans upon request
	 */
		ApplicationContext run =
				SpringApplication.run(FirstProjectApplication.class, args);
		VideoLibrary v=run.getBean(VideoLibrary.class);
		v.InCinema(); // here you will get moviename value as DDLJ
	}

}
```
