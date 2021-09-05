## CDI (Contexts & Dependency Injections) - Java EE dependecy Injection Standard

<b>Contexts:</b> The ability to bind the lifecycle and interactions of stateful components to well-defined but extensible lifecycle contexts <br/>
<b>Dependency injection:</b> The ability to inject components into an application in a typesafe way, including the ability to choose at deployment time which implementation of a particular interface to inject

#### Annotation in CDI

<b>@Named:-</b> Same as @Component in SpringFramework. <br />
<b>@Inject:-</b> Same as @Autowired in SpringFramework. <br />
<b>@Signleton:-</b> It defines the singleton scope of the bean class. 

### Confused CDI or SpringFramework?
If you are using JEE standard then CDI is a good choice but if you are using Dependency Injection context with spring then you can use SpringFramework.

#### How to implement in existing Maven Project

<b>1.</b> Add CDI dependecny in pom.xml<br />
```xml
  <dependency>
     <groupId>javax.inject</groupId>
     <artifactId>javax.inject</artifactId>
     <version>1</version>
  </dependency>
```
<b>2.</b> Save pom.xml. After saving CDI dependencies will be added. <br />
![image](https://user-images.githubusercontent.com/84008107/132124573-d31c0e6a-e47a-4d20-9df5-d7f3e0a21b90.png)

<b>3.</b> Replace @Component with @Named and @Autowired with @Inject in your code and you will get the same output.


