### HAL and the HAL Browser
JSON Hypertext Application Language, or HAL, is a simple format that gives a consistent and easy way to hyperlink between resources in our API. Including HAL within our REST API makes it much more explorable to users as well as being essentially self-documenting.

It works by returning data in JSON format which outlines relevant information about the API.

Dependency

```xml
<dependency>
    <groupId>org.springframework.data</groupId>
    <artifactId>spring-data-rest-hal-browser</artifactId>
    <version>3.3.9.RELEASE</version>
</dependency>
```

URL

http://localhost:8080/browser/index.html
