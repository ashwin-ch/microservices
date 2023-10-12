# Topic: Design Decisions and Development Setup
Q1: Describe list of architecture patterns available in the paper

A: list of microservice patterns described follows below
## API Gateway
> In this pattern, the microservices deployed are managed through a gateway, the interactions between the client and all the other microservice workers/applications. All clients can interfaces with the application for handling tasks such as request routing, authentication, authorization, queue management and transformation through the single point gateway. This pattern has centralized management, better caching, load balancing, request routing, and version handling of the interfaces are easier to migrate with the help of API. Has some downside like single point failure, complexity and latency bottleneck and performance bottleneck and scalability issues. Due to scalability difficulties, the design should be considered how this needs to be materialized in the solution. 
## Service discovery
> This pattern is most adopted in many applications since this enables the ability dynamically locate and communicate with each other. Also to establish direct connection between client and server enabling seemless request/response communication. 
### Client side discovery
    > In this mechanism the client takes the responsibility for identifying which service to create access with, and it queries the service-registery, to select a available server based on its own logic. This also involves load balancing management and service availability. In this, the client takes responsibility of finding the suitable match and managing. The upside is the decentralized client side logic while the downside is the complex client application. 
### Server side discovery
    > The server registers itself into a registry or a directory to establish availability and unregister when the server goes offline. There is no logic on the client side, rather than choosing the service. This mechanism is good for centralized approach for discovery and having reduced logic on client side and the server load becomes more for this mechanism. 

## Hybrid pattern:
> This pattern combines service register together with a message bus replacing a API gateway, which enables routing requests to microservices. The microservices communicates through message, this improves the migration easier and also easier to migrate or deploy the application. The only downside is that, the communication only happens through any adopted message bus, which can become a bottleneck while scaling. 

- Multiple service per host:
> Principle behind this pattern is that, there are multiple services running on a host/node, while it isn't clearly described on if its into the same contrainer or VMs. 
> While having single service per host, has resolved the issue of conflicting dependencies and resources required, providing the ability to isolate of environment from dependencies for any microservice. 

- Database per service
> In this mechanism, each service has its own access to its private database. This has the advantage of simplicity towards migration, from the monolith architecture format. Enables working independent for each service by reducing the dependency.  Also easier to scale using database cluster. 

- Database cluster
> In this pattern, there is cluster of database which is available for microservices to connect, also allows the microservices to have a subset of data to be saved with. This is also known as shared database server. 

- Shared DB server
> In this design pattern, there is only one instance of the database which is accessed by all microservices so there is only one information model/truth mechanism available. This design is simple and allows easier scaling with multiple microservices with various functions being handled/developed. The downside is the traffic, and we need to expand the service resources as the project scales. 


## Q2. How do these patterns differ from the architecture patterns described by Bill Wilder, Cloud Architecture Patterns, O’Reilly, 2012? Are there any similarities?
> The primary idea behind the book is, that, Bill Wilder provides insight to reader on the wholisting cloud architecture schemas and mechanisms and methods for scaling in both horizontal and vertical way. Describes the vertical scaling as more interms of resource and horizontal being expanded by more nodes. The paper more defines about how microservices can be organised with interfaces and communication channels interms of various characteristics and scalability as well. It allows readers to understand what criterias require veritical scaling. For example CDN pattern enables access to data across globe. And allows access for large data model and heavy weight content. 

## Q3. Taibi et al. describe a number of guiding principles for microservice architecture styles. Please list and briefly describe each of these.
In general principles are properties or characteristics embraced while designing, the patterns should contribute these charateristics or principles to an extend and various pattern could contribute to different extent based on nature, and they are
- maintainability
- Possibility to use various programming languages
- flexibility
- Reusability
- Ability to deploy in various methods and models
- Ability to heal
- Overcome failures
- Observability
- Expansion of application functionality and size. 


## Q4. What patterns (from Taibi et al. as well as from Wilder) are currently used in QuoteFinder Version 2?
> The QF application contains two microservices, QFApp and QFWorker having different purpose, and they share one single instance of database, and it denotes that it utilizes shared database server pattern. Also looks like there is Hybrid design pattern deployed based on the message queue created for allocating tasks to the QFWorker from the QFApp. 

## Q5. What are the bottlenecks in the current architecture? What can we do about them?
> Few bottleneck with the implementation is, the shared database server pattern, could cause delay in response and also the socket mechanism for connecting client and server isn't the optimal way, REST API could be used for creating interface which could allow scalability and allow maintenance. 

## Q6. What can be done to scale QuoteFinder Version 2? Think in “both ends”, i.e. scaling the front-end as well as the back-end.
> 1. the database pattern can be improved by migrating to shared cluster pattern, where we reduce the bottleneck of having single instance of database. 
> 2. We can improve the interfaces using RESTFul API for better maintainability and scalability. 
> 3. We can start using json form of exchanging data between, client and server and also between microservices for better debugging and flexibility
These are some thoughts from my mind

