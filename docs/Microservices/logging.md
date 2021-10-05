## Logging

By Enabling logging we can trace the mapped request.

```java
Logger log = LoggerFactory.getLogger(UserController.class); 
	@GetMapping("1")
	public String getUser() throws InterruptedException {
		Thread.sleep(5000);
		//return this.userservice.getUser(userid);
		log.error("Error");
	return "Hello World";
	}
```

To Enable the trace on class level we need to add below properties in application property file

logging.level.root=TRACE

and use log.trace("Tracing");
