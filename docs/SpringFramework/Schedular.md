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

## Example to search a file in a directory on regular interval and if found then move to arch folder.

```java
package com.scheduler.Schedular;

import java.io.*;
import java.nio.file.Files;
import java.nio.file.*;
import org.springframework.scheduling.annotation.Scheduled;

public class Schd {
	
	@Scheduled( cron="*/10 * * * * *")
	public void runningtask() {
		//System.out.println("Running prog");
		//folder
		//delete that 
		
		 		        // Create an object of the File class
		        // Replace the file path with path of the directory
		        File directory = new File("c://Temp//");
		  
		        // store all names with same name
		        // with/without extension
		        String[] flist = directory.list();
		        int flag = 0;
		        if (flist == null) {
		            System.out.println("Empty directory.");
		        }
		        else {
		  
		            // Linear search in the array
		            for (int i = 0; i < flist.length; i++) {
		                String filename = flist[i];
		                if (filename.equalsIgnoreCase("1.txt")) {
		                    System.out.println(filename + " found");
		                    flag = 1;
		                    File file = new File("c:\\Temp\\1.txt");
		                    
		                    // renaming the file and moving it to a new location
		                    if(file.renameTo
		                       (new File("C:\\Temp\\arch\\1.txt")))
		                    {
		                        // if file copied successfully then delete the original file
		                        file.delete();
		                        System.out.println("File moved successfully");
		                    }
		                    else
		                    {
		                        System.out.println("Failed to move the file");
		                    }
		              
		                      
		                }
		            }
		        }
		  
		        if (flag == 0) {
		            System.out.println("File Not Found");
		        }
		    }
	}



```
