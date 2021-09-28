## Let us explore the concepts of microservices through a use-case on Mediamore.com.

Mediamore is an entertainment company which provides streaming media and videos online. It consists of various genres of TV Shows in different languages. Like many other companies mediamore started its journey with a monolithic architecture.

Let us now explore the monolithic framework of mediamore.

### Monolithic Architecture

![image](https://user-images.githubusercontent.com/84008107/135133413-4399393a-89db-4079-974a-ac91149b9c55.png)

Figure 1: Monolithic Architecture of Mediamore – Microservices Tutorial

Refer to the above diagram. We can infer that all the features such as the search, user-info, recommendations, video playlist and others are put on a single database using single code.

Now, let me tell you the challenges faced by the developers while using a monolithic framework by using some scenarios.

### Challenges of Monolithic Architecture
```
Scenario 1: Scalability: Let’s assume that the developers want to update the playlist according to most popular tv shows and also simultaneously want to update all videos to HD quality.

The developers cannot scale the application simultaneously. New instances of the same application have to be created every time a new feature has to be developed or deployed.

Scenario 2: Agility: Assume that developers want to make immediate changes in the application.

The monolithic application can definitely accommodate these changes. But, the problem here is that the developers have to rebuild the code for every small change.

Scenario 3: Hybrid Technologies: Suppose developers of this application are comfortable with various technologies like JAVA, C++,.NET, C#.

Even though they are comfortable with various technologies, they still have to build large and complex applications on a single technology.

Scenario 4: Fault Tolerance: Let’s suppose that a specific feature is not working in the application.

The complete system goes down because of this problem. In order to tackle this problem, the application has to be re-built, re-tested and also re-deployed.

So, how did the developers of mediamore overcome these complexities?

Developers thus decided to re-architect their monolithic application into multiple individual deployable components, called as microservices.

Here lies the million dollar question!
```

### What is Microservices?
Microservices is an architecture wherein all the components of the system are put into individual components, which can be built, deployed, and scaled individually.

Let me explain you with a simple analogy.

You must have seen how bees build their honeycomb by aligning hexagonal wax cells. They initially start with a small section using various materials and continue to build a large beehive out of it. These cells form a pattern resulting in a strong structure which holds together a particular section of the beehive. Here, each cell is independent of the other but it is also correlated with the other cells. This means that damage to one cell does not damage the other cells, so, bees can reconstruct these cells without impacting the complete beehive.

![image](https://user-images.githubusercontent.com/84008107/135133573-ef2cfe8e-49b6-4d4d-bfbd-e579459e71d0.png)

Refer to the above diagram. Here, each hexagonal shape represents an individual service component. Similar to the working of bees, each agile team builds an individual service component with the available frameworks and the chosen technology stack. Just as in a beehive, each service component forms a strong microservice architecture to provide better scalability. Also, issues with each service component can be handled individually by the agile team with no or minimal impact on the entire application.

The next question that may come to your mind is how do the different components of microservice architecture work together.

But, before that, let me list down the components of the microservice architecture.

Refer to the below diagram.

![image](https://user-images.githubusercontent.com/84008107/135133678-f6024efd-34de-49ef-97e8-f49e91665da1.png)

```
Clients – Different users from various devices send requests. 
Identity Providers – Authenticates user or clients identities and issues security tokens.
API Gateway – Handles client requests.
Static Content – Houses all the content of the system.
Management –  Balances services on nodes and identifies failures.
Service Discovery – A guide to find the route of communication between microservices.
Content Delivery Networks – Distributed network of proxy servers and their data centers.
Remote Service – Enables the remote access information that resides on a network of IT devices.
```
### Microservice Architecture
```
Scenario:
Alice is an avid user of mediamore. She uses mediamore regularly to watch her favorite series online. She recently missed watching an episode of her favorite TV show. 

When Alice logs in to the application, she sees the most recommended content on her home page. After some searching, she finally finds her TV Show.

But, what if Alice wants to get her TV Show with a single click.

How will the developers work together to fulfill Alice’s request?

Alice’s request is passed on to the Identity Provider. Identity provider thus authenticates Alice’s request by identifying her as a regular user on mediamore. 

These requests are passed to the API Gateway which acts as an entry point for Alice to forward her requests to the appropriate microservices.

Each feature has its own working microservice, handling their own data. These microservices also have their own load balancers and execution environments to function properly. 
```
![image](https://user-images.githubusercontent.com/84008107/135133900-52e65bbb-36d2-45ef-8de3-8d7874bf0741.png)

Figure 5: Division of Teams of Mediamore – Microservices Tutorial

```
The content team consists of millions of TV Shows that the application provides.
The video uploading team have the responsibility to upload all the content into the application
The most trending team houses the most trending shows according to the geographical location of users and so on.
These small teams of developers relate each and every piece of content with the metadata that describes the searched content. Then, metadata is fed into another microservice i.e. the search function which ensures Alice’s search results are captures into the content catalog.

Then, the third microservice i.e. most trending microservice captures the trending content among all the mediamore users according to their geographical locations.

The content from this microservice is what Alice sees when she first logs into mediamore.

These individually deployable microservices are put in specific containers to join the application. Containers are used to deliver the code to the sector where deployment is required. 

But before they join the application to work together, they have to find each other to fulfil Alice’s request.

How do these microservices find each other?

Microservices use service discovery which acts as a guide to find the route of communication between each of them. Microservices then communicate with each other via a stateless server i.e. either by HTTP Request/Message Bus.
```
![image](https://user-images.githubusercontent.com/84008107/135134018-1d43bd22-bc8e-4f59-91e1-a178b72c8a8a.png)

```
Figure 6: Communication Between Microservices – Microservices Tutorial

These microservices communicate with each other using an Application Program Interface(API). After the Microservices communicate within themselves, they deploy the static content to a cloud-based storage service that can deliver them directly to the clients via Content Delivery Networks (CDNs).

 

So, when Alice searches for her TV Show, the search microservice communicates with the content catalog service in API about what is Alice searching for and then these microservices compare the typed words with the metadata they already have.
```
![image](https://user-images.githubusercontent.com/84008107/135134169-94fd757e-90a0-4213-a3e9-72a9a0f79f42.png)

Figure 7: Representation of how to search operation is performed with the help of API  – Microservices Tutorial

Once the teams of developers capture the most typed words by Alice, the analytics team update the code in recommendations microservice and compare Alice’s most viewed content and preferences to popular content among other users in the same geographical region.
