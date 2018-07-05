# microservice

Microservices involve an architectural approach that emphasizes the decomposition of applications into single- purpose, highly cohesive and loosely coupled services managed by cross-functional teams, for delivering and maintaining complex software systems with the velocity and quality required by today’s digital businesses.

Microservices are language-, platform-, and operating system-agnostic.

Each microservice is generally built by a full-stack team.

# Key characteristics of microservices

1. [Domain-Driven Design](TODO). Functional decomposition can be easily achieved using Eric Evans’s DDD approach.
1. __Single Responsibility Principle__. Each service is responsible for a single part of the functionality, and does it well.
1. __Explicitly Published Interface__. A producer service publishes an interface that is used by a consumer service.
4. __Independent DURS__ (Deploy, Update, Replace, Scale). Each service can be independently deployed, updated, replaced, and scaled.
5. __Smart Endpoints and Dumb Pipes__. Each microservice owns its domain logic and communicates with others through simple protocols such as REST over HTTP.

# Benefits

* Independent scaling - on X-axis (more CPU or memory) or Y-axis (sharding / partitioning)
* Independent upgrades / deployments - can change without coordination, enabler CI/CD
* Easy maintenance
* Potential heterogeneity and polyglotism - pick the best language suited for a service, free to innovate within the confines of their service. This enables one to rewrite the service using newer technologies as opposed to being penalized because of past decisions, and gives freedom of choice when picking a technology, tool, or framework
* Fault and resource isolation
* Improved communication across (full-stack) teams

# Operational requirements

* Service replication
* Service discovery - due to container based platform, services may scale up and down: the exact address of a service may not be known until the service is deployed and ready to be used. Each service registers with a broker and provides more details about itself ([Kubernetes](TODO) makes service discoverability very easy)
* Service monitoring - Elasticsearch, Fluentd, and Kibana can aggregate logs from different microservices, provide a consistent visualization over them, and make that data available to business users
* Resiliency - Software failure will occur (no matter how much and how hard you test): The key concern is not "how to avoid failure" but "how to deal with failure.". It’s important for services to automatically take corrective action to ensure user experience is not impacted. The Circuit Breaker pattern allows one to build resiliency in software
* DevOps - CI/ CD are very important in order for microservices-based applications to succeed

# Good Design Principles on monolith

1. Separate your concerns (MVC, API...)
1. Convention over Configuration
1. Follow the Law of Demeter (Each unit should have only limited knowledge/talk about other units)
1. Domain-Driven Design
1. Automation
1. Design to Interfaces / APIs (high cohesion / low coupling)
1. Group code by functionality, not by layer
1. Make your code stateless and externalize your application’s state

# Patterns

* Use Bounded Contexts (from [DDD](TODO)) to identify candidates for microservices. The use of an anti-corruption layer is strongly recommended during the process of decomposing a monolith.
* Designing frontends for microservices
* Use an API gateway to centralize access to microservices
* Database design and refactorings - Unlike a monolithic application, which can be designed to use a single database, microservices should be designed to use a separate logical database for each microservice.
* Packaging and deploying services - Consider the use of virtualization technologies that allow
the tech stacks / microservice to be packaged and deployed in separate virtual environments (consider the use of a container orchestration technology like [Kubernetes](TODO))
* Event-driven architecture - for the eventual consistency of a microservices architecture, consider the use of an event-driven architecture where data-changes in one microservice are relayed to interested microservices through events
* Consumer-Driven contract testing - To account for the eventual consistency property of a microservices architecture, one should consider the use of an event-driven architecture where data-changes in one microservice are relayed to interested microservices through events.

# Resources

- Gewtting Started with Microservices - DZone Refcardz