## Caching
@Cacheable annotation that’s used to mark methods whose return values will be stored in a cache.

Like @Cacheable, @CacheEvict has value, key and condition attributes and it clears the caching on the basis of cache key.

### Steps

1. Add the dependency

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-cache</artifactId>
    
</dependency>
```

2. Enable Caching on Application class level
3. Add Caching as given below @EnableCaching

```java
@GetMapping("1")
	@Cacheable("hello")
	public String getUser() throws InterruptedException {
		Thread.sleep(5000);
		//return this.userservice.getUser(userid);
	return "Hello World";
	}
	
	@GetMapping("2")
	@CacheEvict("hello")
	public String getUse1r()  {
		
		//return this.userservice.getUser(userid);
	return "Done";
	}
```


