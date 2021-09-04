## @ComponentScan 
Using component scan is one method of asking Spring to detect Spring-managed components. Spring needs the information to locate and register all the Spring components with the application context when the application starts. Spring can auto scan, detect, and instantiate components from pre-defined project packages.

### Example
Create a package <b>com.kmit.spring.scan</b> which is outside the FirstProject package and create following Bean Classes

#### ScanComponent.java
```java
package com.kmit.spring.scan;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public  class ScanComponent {
	
	@Autowired
	SubComponent sub1;
	public void ScanMethod() {
		sub1.scan();
	}
}

```
#### SubComponent.java
```java
package com.kmit.spring.scan;

import org.springframework.stereotype.Component;

@Component
public abstract class SubComponent {

	abstract void scan();

}

```
#### SubComponent1.java
```java
package com.kmit.spring.scan;

import org.springframework.stereotype.Component;

@Component
public class SubComponent1 extends SubComponent{

	@Override
	void scan() {
		// TODO Auto-generated method stub
		System.out.println("SubComponent1");
	}

}
```
#### Call these Bean classes in FirstProject namespace,
you need to use @ComponentScan("com.kmit.spring.scan") otherwise springframework will not able to find the ScanComponent and other classes, because by default application context is for current package.

```java
package com.kmit.spring.FirstProject;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;
import org.springframework.context.ConfigurableApplicationContext;
import org.springframework.context.annotation.ComponentScan;

import com.kmit.spring.scan.ScanComponent;
@SpringBootApplication
@ComponentScan("com.kmit.spring.scan")
public class FirstProjectApplication {

	public static void main(String[] args) {
	/* ApplicationContext can load bean definitions, wire beans together
	 * , and dispense beans upon request
	 */
		ApplicationContext run =
				SpringApplication.run(FirstProjectApplication.class, args);
		ScanComponent c1=run.getBean(ScanComponent.class);
		c1.ScanMethod();
		}

}

```
