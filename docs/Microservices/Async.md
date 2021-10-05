## Async
Simply put, annotating a method of a bean with @Async will make it execute in a separate thread. In other words, the caller will not wait for the completion of the called method.

@EnableAsync on application level

### Example

```java
package com.client;

import org.springframework.scheduling.annotation.Async;
import org.springframework.stereotype.Service;

@Service
public class notifservice {
	@Async
	public void sendmsg() throws InterruptedException
	{
		Thread.sleep(30000);
		System.out.println("Message is sent");
	}
}

```


### Call the method in a controller

```java
package com.client;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.cache.annotation.CacheEvict;
import org.springframework.cache.annotation.Cacheable;
import org.springframework.scheduling.annotation.Async;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.client.RestTemplate;

import com.sun.org.slf4j.internal.Logger;
import com.sun.org.slf4j.internal.LoggerFactory;





@RestController
@RequestMapping("/user")
public class UserController {


	@Autowired
	notifservice n= new notifservice();
	@GetMapping("1")
	public String getUser() throws InterruptedException  {
		
		
		n.sendmsg();
		//return this.userservice.getUser(userid);
		//log.trace("test");
	return "Hello World";
	}
	
		
}

```
