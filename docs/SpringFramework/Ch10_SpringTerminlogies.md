# Spring Terminology
### IOC (Inversion of Control)
An IoC container is a common characteristic of frameworks that implement IoC. In the Spring framework, the interface ApplicationContext represents the IoC container. The Spring container is responsible for instantiating, configuring and assembling objects known as beans(@Component) and Dependencies(@Autowired), as well as managing their life cycles.

### Bean Factory
This is the simplest container providing the basic support for DI and defined by the org.springframework.beans.factory.BeanFactory interface. The BeanFactory and related interfaces, such as BeanFactoryAware, InitializingBean, DisposableBean, are still present in Spring for the purpose of backward compatibility with a large number of third-party frameworks that integrate with Spring.

### ApplicationContext (Mostly used instead of Bean Factory)
It includes all the feature of Bean Factory.The most commonly used ApplicationContext implementations are −

<b>FileSystemXmlApplicationContext −</b> This container loads the definitions of the beans from an XML file. Here you need to provide the full path of the XML bean configuration file to the constructor.

<b>ClassPathXmlApplicationContext −</b> This container loads the definitions of the beans from an XML file. Here you do not need to provide the full path of the XML file but you need to set CLASSPATH properly because this container will look like bean configuration XML file in CLASSPATH.

<b>WebXmlApplicationContext −</b> This container loads the XML file with definitions of all beans from within a web application. 

