## Why are Microservices used?
Microservices were used to overcome the challenges of monolithic architecture that prevailed initially in the market and also enables you to deploy independent services.

So, before we move on to what is Microservices in simple words, let’s see the architecture that prevailed initially in the market i.e. the Monolithic Architecture.

In layman terms, you can say that its similar to a big container wherein all the software components of an application are assembled together and tightly packaged.

![image](https://user-images.githubusercontent.com/84008107/135131892-71a31a2d-475a-4b36-a105-437352b320f0.png)

```
Inflexible – Monolithic applications cannot be built using different technologies 
Unreliable – Even if one feature of the system does not work, then the entire system does not work
Unscalable – Applications cannot be scaled easily since each time the application needs to be updated, the complete system has to be rebuilt
Blocks Continous Development – Many features of the applications cannot be built and deployed at the same time
Slow Development – Development in monolithic applications take lot of time to be built since each and every feature has to be built one after the other
Not Fit For Complex Applications – Features of complex applications have tightly coupled dependencies
The above challenges were the main reasons that led to the evolution of microservices. So, now let us understand what is Microservices in simple words?
```

### What exactly is Microservices?
Microservices is an architectural style that structures an application as a collection of small autonomous services, modeled around a business domain.

![image](https://user-images.githubusercontent.com/84008107/135132049-4bc612c6-1003-4b25-b7ab-88bd296e5173.png)

In the given Architecture, each service is self-contained and implements a single business capability.

### Differences Between Traditional Architecture and Microservices
Consider an E-commerce application as a use-case to understand the difference between both of them.

![image](https://user-images.githubusercontent.com/84008107/135132167-d01fe399-b6ac-4cce-9058-d0f86de12030.png)
Figure 3: Differences Between Monolithic Architecture and Microservices

The main difference we observe in the above diagram is that all the features initially were under a single instance sharing a single database. But then, with microservices, each feature was allotted a different microservice, handling their own data, and performing different functionalities. 

### Architecture of Microservices

![image](https://user-images.githubusercontent.com/84008107/135132301-4e1827d9-68ee-44a9-87d1-c981b938cff7.png)

```
Different clients from different devices try to use different services like search, build, configure and other management capabilities
All the services are separated based on their domains and functionalities and  are further allotted to individual microservices
These microservices have their own load balancer and execution environment to execute their functionalities & at the same time captures data in their own databases
All the microservices communicate with each other through a stateless server which is either REST or Message Bus
Microservices know their path of communication with the help of Service Discovery and perform operational capabilities such as automation, monitoring
Then all the functionalities performed by microservices are communicated to clients via API Gateway
All the internal points are connected from the API Gateway. So, anybody who connects to the API Gateway automatically gets connected to the complete system
```

### Microservices Features

![image](https://user-images.githubusercontent.com/84008107/135132397-cb982b40-fcc7-4b5f-9b55-640589fa5b26.png)

```
Decoupling – Services within a system are largely decoupled. So the application as a whole can be easily built, altered, and scaled
Componentization – Microservices are treated as independent components that can be easily replaced and upgraded
Business Capabilities – Microservices are very simple and focus on a single capability 
Autonomy – Developers and teams can work independently of each other, thus increasing speed
Continous Delivery – Allows frequent releases of software, through systematic automation of software creation, testing, and approval 
Responsibility – Microservices do not focus on applications as projects. Instead, they treat applications as products for which they are responsible 
Decentralized Governance – The focus is on using the right tool for the right job. That means there is no standardized pattern or any technology pattern. Developers have the freedom to choose the best useful tools to solve their problems 
Agility – Any new feature can be quickly developed and discarded again
```

### Advantages Of Microservices

![image](https://user-images.githubusercontent.com/84008107/135132476-b8bd141c-b411-45b1-902a-206e85633e87.png)

```
Independent Development – All microservices can be easily developed based on their individual functionality
Independent Deployment – Based on their services, they can be individually deployed in any application 
Fault Isolation – Even if one service of the application does not work, the system still continues to function
Mixed Technology Stack – Different languages and technologies can be used to build different services of the same application
Granular Scaling –  Individual components can scale as per need, there is no need to scale all components together
```
