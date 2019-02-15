## General
1. This book is about how you decompose an enterprise application into layers and how these layers work together.
2. This book in general deals with Enterprise Applications i.e. applications that deals with huge and complex data.
3. Enterprise Applications include payroll, patient records, shipping tracking, cost analysis, credit scoring, insurance, supply chain, accounting, customer service  and foreign exchange trades.
4. Enterprise Applications don't include automobile fuel injection, word processor, elevator controllers, chemical plant controllers, telephone switches, operating systems, compilers and games.
5. Enterprise Applications usually involve persistent data. Data is persistent because it needs to be available for multiple runs of the programs and in most cases for many years to come.
6. Enterprise Applications usually need to integrate with other applications.
7. Choosing an architecture for an enterprise app. will depend upon the type of the appl., for instance a b2c online retailer will have a different arch. from an system that automates the processing of leasing agreements and this will be different from an app., like that of an expense tracking system which might have to be integrated with other applications or might have to make webservice calls to consume data from an airline ticketing system.
8. Many architectural decisions are about performance.
9. For most performance issues, the preferred way is to get to the system up and running, instrument it, and then use disciplined optimization process based on measurement.
10. Response time: is the amount of time a system takes to process a request from the outside. This may be a UI action, like clicking a button or a server API call.
11. Responsiveness: is about how quickly a system acknowledges a request as opposed to processing it. This is imp. because in many systems users become frustrated if a system has low responsiveness even if the response time is good. Providing a progress bar during file copy is an example of good responsiveness.
12. Latency: is the minimum time required to get any form of response. An application dev can't do much about latency because it depends upon the request and response speeds between networks, the best way is to keep remote calls as minimal as possible.
13. Throughput: is how much stuff you can do in a given amount of time. For a file copy, it's measured in bytes per sec whereas in an enterprise app. it is measured as transactions per second.
14. Performance can be about Response time or Responsiveness or Throughput. From a user perspective, responsiveness is crucial.
15. Load: is about how much stress a system is under which maybe no.of users connected to the system right now. Response Time and Load are used together. For e.g., the response time of a system could be 0.5 seconds w/ 10 users and 2 seconds w/ 20 users.
16. Load Sensitivity: is an expression of how the response time varies w/ load.
17. Efficiency is performance divided by resources. A system that can get 30 tps on 2 cpu's is more efficient than a system that can get 40 tps on 4 identical cpu's. 
18. Capacity of an system is the maximum effective throughput or load a system can take above which the performance dips below acceptable threshold.
19. Scalability is a measure of how adding resources (usually hardware) affects performance. A scalable system is one which allows you to add hardware and get a increase in performance.
20. Vertical Scalability means adding more power to a single server such as more memory. Also called as scaling up.
21. Horizontal Scalability means adding more servers. Also called as scaling out.
22. When building enterprise applications, it is often better to build for hardware scalability rather than capacity or even efficiency. Because scalability gives the option to increase performance if needed and it is easier to do.
23. Often designers do complicated things that will improve the capacity on a particular hardware platform when it might actually be cheaper to buy ore hardware.
24. Patterns: each pattern describes a problem which occurs over and over again and then describes the core of a solution to that problem in such a way that you can use this solution a millions times over w/o ever doing it the same way twice.
25. The key thing about patterns is that they do not offer a complete solution which you can apply blindly, that is why they fail miserably. Patterns are half-baked solutions and every time you apply one of these you will have to fill-in with your own tweak to solve the problem.
26. But it's important to first identify which pattern to apply and then apply your engineering skills to tweak it to solve the problem.
27. Each pattern is relatively independent but patterns are not isolated from each other. Often one pattern leads to another or one occurs only if another is around.
28. The best way to remember patterns is to draw a sketch using UML diagram or something similar.
29. This book is not a exhaustive list of patterns. You yourself will come across many patterns as you look at more and more enterprise applications and hopefully can come up with suitable solutions that can be applied to similar repeating patterns.
<br/>

## Layering
1. Advantages of breaking down a system into layers are as follows.
2. you can understand one layer w/o knowing the full details of the other layers. for e.g. you can work w/ UI part w/o understanding the db part.
3. you can replace one layer w/ other compatible layer.
4. you can minimize dependencies b/w layers and make changes to only one layer w/o affecting others.
5. Disadvantages of layering are as follows;
6. this can introduce cascading effects. If you want to add a field on the UI layer, you will also have to add in the business logic and in the database. This change goes into every layer.
7. extra layers can harm performance.
8. The most important thing w/ layering is to decide which layers to have and what the resposnbility of each layer should be.
<br/>

## Evolution of Layers in Enterprise Applications
1. Started w/ Client-Server systems. Two-layered arch.
2. The client held the UI and other application code and the server was usually a relational db.
3. If the application was all aboout display and update of simple relational data then this 2-layered arch was enough.
4. For systems that had domain logic like business rules, validations, calculations etc. the 2-layered arch was not enough since you can't write the domain logic in the client code and couple it w/ the UI code. And hence, people started putting the domain logic inside the db using stored procs and triggers which gives limited structring mechanisms and hard to maintain code.
5. In order to solve this, 3-layered systems were introduced. One layer for the UI, the other for the domain logic and the third for the data source.
6. Generally, layer and tier are synonymous. But tier is more seen as a physical separation as in the case of a client and a server.
<br/>

## The Three Principal Layers
1. This book focuses on presentation, domain and data source layers.
2. Primary responsibility of the Presentation layer is to display information and capture requests from user using the rich UI. Acts as an interface b/w the user and the system.
3. Data Source logic is about communicating w/ other systems that perform some tasks on behalf of this application such as other applications, messaging systems or in most systems it is the simple rdbms which persists data.
4. Domain logic also known as business logic is the crux of the business which carries out business rules, validations and decides what data source logic to dispatch for which request.
5. A single application can have multiple packages of each layer i.e. a system can have a command-line UI and also a rich UI presentation layer. Similaryly multiple data sources.
6. Domain and Data Source should never be dependent on the presentation in such a way that anytime down the line the presentation layer be changed w/ a different library altogether w/o any ramifications on the domain and data source.
7. Distribution, explicit multithreading, object/relational paradigms, multiplatform development and extreme performance optimization (such as 100 tps) are all complexity boosters. All carry a cost.
<br/>

# DOMAIN LOGIC PATTERNS
1. Domain Logic can be organized into 3 primary patterns.
2. They are : Transaction Script, Domain Model and Table Module.
<br/>

