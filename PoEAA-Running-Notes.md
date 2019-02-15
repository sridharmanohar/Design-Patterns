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

## Transaction Script
1. This is the simplest way of storing domain logic.
2. A Transaction Script is basically a procedure which takes inputs from the presentation, processes it w/ validations and calculations, stores the data in the db and throws the desired result back to the presentation.
3. A Transaction Script need not be a single procedure, it can be one procedure calling another, basically you have one procedure for one action.
4. This is a simple model and easy to understand.
5. This works well w/ simple data source layer using Row Data Gateway or Table Data Gateway.
6. This model does not serve well when the logic is complex.
<br/>

## Domain Model
1. In this, we build a model of our domain i.e. we create classes around the nouns of the domain.
2. For e.g., a leasing system will have classes for lease, asset etc.
3. Logic for validations and calculations will be put in the domain model.
4. Domain Model usually deals w/ a Data Mapper for db mapping part.
<br/>

## Table Module
1. A Table Module is designed to work w/ Record Set.
2. This is a kind of a middle ground b/w a Transaction Script and a Domain Model.
3. Particularly .NET based applications use this approach.
<br/>

## How to choose b/w a Transaction Script vs Domain Model vs Table Module
1. First of all these 3 are not mutually exclusive choices. It's quite common to use Transaction scripts for some part of the domain logic and Domain Model for the rest.
2. But, generally speaking, Transaction Script and Table Module will become quite difficult to scale as the domain logic becomes complex.
3. For simple domain logic, Transaction Scripts is a good starting point.
4. Most applications use a combination of Transaction Script and Domain Model.
<br/>

## Service Layer
1. A common approach to handling domain logic is to split the layer into 2.
2. A Service Layer sits on top of either a Domain Model or a Table Module. Transaction Script models are anyways simple and hence do no need this split.
3. The presentation logic deals w/ the domain logic only through the Service Layer, that is, this acts as an API for the application.
4. Service layer is also a good place to handle Security and Transaction Control.
5. A key decision w/ Service Layer is to understand how much behaviour to put in it.
6. In its minimilastic sense, a Service layer can act as a facade and all it does is to forward calls to the underlying lower-level objects. Here it acts as an API and also provides a good place to put in security checks and transactional wrappers.
7. Service Layer generally shouldn't have any business logic.
8. Preference is to have a Service Layer (only if you need one). Although, many designers always use a Service Layer w/ good bit of logic in it. So, some people prefer to have a rich Service Layer.
<br/>

# DATA SOURCE ARCHITECTURAL PATTERNS
1. It's always good to separate SQL code from the domain logic and put it in separate classes.
2. On way to organize these classes is to base them on the db tables i.e. one class per table and put all the SQl code in the relative classes.
3. These classes then form a Gateway.
4. Table Data Gateway, Row Data Gateway, Active Record and Data Mapper are the data source patterns that are talked about in this book.
<br/>

## Row Data Gateway
1. An object that acts as a Gateway to a single record in a data source.
2. There is one instance per row.
3. A Row Data Gateway gives you objects that looks exactly like the record in the record structure but can be accessed w/ the regular mechanisms of your programming language.
4. An RDG basically represents a single row in a table.
5. Members of RDG can be either data attributes that correspond exactly to the columns of the table in question and/or methods which handle querying the db.
6. In an RDG there are no methods which aren't either getters/setters or SQL. The moment you add any domain logic in an RDG, it becomes an Active Record.
7. https://richard.jp.leguen.ca/tutoring/soen343-f2010/tutorials/implementing-row-data-gateway/
<br/>

## Active Record
1. The only difference b/w an Active Record and an RDG is that an Active Record will contain domain logic as well.
2. The problem w/ AR is that it has responsibilities which spans across the Domain layer and the Data Source layer.
3. Ideally not preferred in java world.
4. https://richard.jp.leguen.ca/tutoring/soen343-f2010/tutorials/implementing-active-record/
<br/>

## Data Mapper
1. The solution to an Active Record is to split it into two - one as a domain model and another as a data mapper.
2. But one problem w/ this is there will be a (upward) dependency from the Data Mapper to the Domain Model. And for that dependency to go the Data Mapper has to move into the Domain Layer but that can't happen so long as the Data mapper is coupled to the SQL.
3. If you are using a Domain Model then it is always better to have an O/R mapping tool because building a Data Mapper on your own is a complicated behavior.
4. https://richard.jp.leguen.ca/tutoring/soen343-f2010/tutorials/implementing-data-mapper/
<br/>

## Table Data Gateway
1. An object that acts as a Gateway to a db table. One instance handles all rows in the table.
2. A TDG holds all the sql for accessing a single table or view: selects, inserts, updates and deletes. Other code calls its methods for all interfactions w/ the db.  
3. TDG fits very nicely w/ Record Set.
4. If you are using a Table Module, then TDG w/ Record Set is a good choice.
5. If you are using Domain Model, you can go w/ either RDG or a TDG.
6. If the domain logic is simple and there is close correspondence to classes and tables then you can go w/ Active Record rather than using a Gateway.
7. If the Domain logic is complex, then Data mapper is kind of an appropriate option for Domain Model.
8. https://richard.jp.leguen.ca/tutoring/soen343-f2010/tutorials/implementing-table-data-gateway/
<br/>

# OBJECT-RELATIONAL BEHAVIORAL PATTERNS
1. The major difficulty when it comes to O/R mapping is its behavioral problem i.e. how to get the various objects to load and save themselves to the db.
2. When you load many objects you should ensure concurrency is handled, state is maintained and referential integrity is also handled before you commit them back.
3. Some patterns that deal w/ these behavioral issues are Unit of Work, Identity Map and Lazy Load.
<br/>

## Unit of Work
1. A UoW keeps track of all objects read from the db, together w/ all objects modified in any way.
2. It also handles how updates are made to the db.
3. Instead of the application prmgr explcitly invoking save, we tell the UoW to commit. The UoW then puts all the operations to be performed in a sequence and performs it.
4. W/o a UoW, typically the domain layer acts as a controller, deciding when to read and write to the db.
5. A UoW basically maintains a list of objects affected by a business transaction and coordinates the writing out of changes and the resolution of concurrency problems.
<br/>

## Identity Map
1. When you load objects you need to be careful that you are not loading the same one twice. If this happens, that means, there is more than one in-memory object that corresponds to the same db row and when you update such a thing, things will go wrong.
2. In order to prevent this from happening, every time you read you need to keep a record of that in the Identity Map.
3. Each time you read in some data, first check IM to see this does not already exists in it, If yes, then return a second reference to the same one, that way all updates are properly coordinated.
4. Another benefit of an IM is you will not be doing unnecessary db calls.
5. But the primary purpose of an IM is to maintain correct identities and not to boost performance.
6. So, an IM basically keeps track of all objects that have been read from the db in a single business transaction.
<br/>

## Lazy Load
1. If you are using Domain Model, things are generally arranged in such a way that, when you load one object all it's associated objects also are automatically objects. This can lead to memory/performance issues.
2. W/ Lazy Loading, only what needs gets loaded at the same time keeping the gate open to load others as and when required.
3. There are 4 varieties of Lazy Loading: Lazy initialization, Virtual proxy, Value Holder and Ghost.
<br/>

## Reading in Data
1. Some rule of thumb while reading data in order to avoid performance issues are as follows.
2. Try to pull multiple rows at once. Don't do multiple queries on the same table to get multiple rows. It's almost always better to pull back too much data than too little.
3. Another way to avoid going to the db again and again is to use joins. Using joins you get data from multiple related tables all in one go. Although the resulting record set might look odd but this will definitely speed things up.
4. However, one thing about joins is, db's are generally optimized to handle 3 to 4 joins per query beyond which performance will take a hit.
<br/>

