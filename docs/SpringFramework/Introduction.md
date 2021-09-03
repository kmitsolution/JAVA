# Spring Framework


  <b> Repository:</b> github.com/spring-projects/spring-framework </br>
  <b> Developer(s):</b> Pivotal Software </br>
  <b> Initial release:</b> 1 October 2002 </br>
  <b> License:</b> Apache License 2.0 </br>
  <b> Platform:</b> Java EE</br>
  <b> Stable release:</b> 5.3.8 / 9 June 2021</br>

## What is Spring Framework (Dependency Injection Framework)
<ul>
  <li> The Spring Framework is an application framework and inversion of control container for the Java platform. </li>
  <li> The Spring Framework (Spring) is an open-source application framework that provides infrastructure support for developing Java applications.</li>
  <li> The framework's core features can be used by any Java application, but there are extensions for building web applications on top of the Java EE platform.</li>
</ul>  

### Example of Dependency 
In a video library there is collection of Hollywood and Bollywood movies and seller is selling either of these movies and also in future any new category of movies can be added to the collection.
Let's solve this by creating java classes as mentioned below
```java
      public class VideoLibrary{
        Movies movies;
        public VideoLibrary() {
         movies = new BollywoodMovies(); //movies variable is 
        }
        public void InCinema()
        {
           movies.watch();
        }
        public static void main(String[] args) {
           
            v1.InCinema(); // It will print Watching Bollywood Movie

	      }
      }

      abstract class Movies{

      }
      abstract class Movies{
        abstract void watch();
      }
      class BollywoodMovies extends Movies {

        @Override
        void watch() {
          System.out.println("Watching Bollywood Movie");

        }

      }

      class HollywoodMovies extends Movies {

        @Override
        void watch() {
          System.out.println("Watching Hollywood Movie");

        }

```

#### Problem in above code
<p>In above example <b>VideoLibrary</b> class is dependent on Movies class(tightly coupled), which cause a problem like if we need to refer <b>HollywoodMovies</b></p> Then we need to change the definition of VideoLibrary.</p>

#### Solution 
<p> To handle the above code dependency, the best way to create a parameterized constructor by passing Movies parameter</p>


```java
   public class VideoLibrary {
         Movies movies; 
     public VideoLibrary(Movies watchmovie) { //Created a parameterized constructor for loosely couple
         movies = watchmovie;
           }
         
     public void InCinema() {
         movies.watch();
           }

      public static void main(String[] args) {
         Movies bollywood = new BollywoodMovies();
         VideoLibrary v1= new VideoLibrary(bollywood);
         v1.InCinema();

            }

}
```
### Spring Framework
  Spring Framework Identifies the dependencies using Dependency Injection. 



