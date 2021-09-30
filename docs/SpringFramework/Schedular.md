### Step 1 :- Create Simple SpringBoot project
1. Create Default Spring Project using Spring Initializr https://start.spring.io/
2. Import project in Eclipse
3. Create SchedularConfig and Schedular class

```java
package com.schedular.Schedular;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.scheduling.annotation.EnableScheduling;

@Configuration
@EnableScheduling
public class ScheduleConfig {

	@Bean
	public Schd schedule() {
		return new Schd(); 
	}
}
```

```java
package com.schedular.Schedular;

import org.springframework.scheduling.annotation.Scheduled;

public class Schd {
	
	@Scheduled( fixedDelay =1000)
	public void runningtask() {
		System.out.println("Running prog");
	}

}

```

## You can use cron option also

```java
package com.schedular.Schedular;

import org.springframework.scheduling.annotation.Scheduled;

public class Schd {
	
	@Scheduled(cron = "* * * * * *")
	public void runningtask() {
		System.out.println("Running prog");
	}

}

```
