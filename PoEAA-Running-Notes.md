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

# OBJECT-RELATIONAL STRUCTURAL PATTERNS
1. When talking about O/R mapping it is these structural patterns which are generally talked about in order to map in-memory objects and db tables.
2. These patterns aren't usually relevant to TDG, but you may use a few of them for RDG or Active Record.
3. You will probably need all of them when using a Data Mapper.
4. These patterns are : Identity Field, Foreign key Mapping, Association Table Mapping, Dependent Mapping, Embedded Value, Serialized LOB, Single Table Inheritance, Class Table Inheritance, Concrete Table Inheritance, Inheritance Mappers.
<br/>

## Identity Field
1. This basically saves the database ID field in an object in order to maintain identity b/w an in-memory object and a db row.
2. All you do is store the primary key of the db row in the object's field.
<br/>

## Foreign Key Mapping
1. A Foreign Key Mapping maps an object reference to a foreign key in the db.

## Association Table Mapping
1. This is basically to deal w/ many-to-many associations.
2. This is like an object having a collection as one of its fields.
3. For e.g. an Employee can have multiple Skills and one skill can be associated w/ multiple employees. To map such a thing, let's say, there is an Employees table w/ all employee details and a Skills table w/ all skills, then a skill-employee table will contain many-to-many mapping. This is called ATM.
<br/>

## Embedded Value
1. This is about mapping a field of an object into several fields of a table.
2. FOr instance, your object has a field called dateRange, you can split this into start date and end date fields in the db table since you won't have a dataRange data type in the db table.
<br/>

## Serialized LOB
1. Saves a graph of objects by serializing them in a single large object, which it stores in a db field.
2. Objects dont have to be persisted as table rows related to each other. Another form of persistence is serialization, where a whole graph of objects is written out as a single large object (LOB) in a table.
3. These LOBs can be saved as BLOB or CLOB.
4. Hierarchical structures such as org. charts and bills of materials are where a Serialized LOB can save a lot of db trips.
5. But the downside is that the SQL isn't aware of what is happening, so you can't make portable queries against the data structure.
6. Serialized LOBs are best used when you dont want to query for the stored structure.
7. Usually this is best suited for relatively isolated group of objects that make part of an application.
8. If you use it too much it ends up turning your db in a mere transactional file system.
<br/>

## Working with Collections
1. Using unordered sets while using collections is better when you have to write the data back to the db.
2. Also systems which defer referential integrity checking to the end of the transaction is also better otherwise the db will check on every write.
<br/>

## Inheritance
1. A class hierarchy linked by inheritance can't be just represented in a db because there is no inheritance in sql.
2. For any inheritance structure there are 3 options: Single Table Inheritance, Concrete Table Inheritance and Class Table Inheritance.
3. STI: one table for all classes in the hierarchy i.e. all fields in all the classes of the hierarchy will be put in only one table.
4. CoTI: one table for each concrete class in the hierarchy.
5. CaTI: one table for each class in the hierarchy.
6. The trade-offs b/w these options is b/w duplication of data structures and speed of access.
7. CaTI is the simplest, but it needs multiple joins to load a single object which can affect performance.
8. CoTI avoid joins allowing you to pull a single object from one table but it is brittle to changes. Any changes to the super class and we have to remember to alter all the tables.
9. CoTI: The lack of superclass table can make key management awkward and can get in the way of referential integrity.
10. STI: biggest downside is it's wasted space. Since one table will have to have all the cols of all classes, some cols for some rows will have no data and that will lead to wasted space.
11. All 3 options are not mutually exclusive. You can make some classes to have STI and some to have CaTI.
12. There is no clear cut winner amongst these 3 options.
13. CoTI: includes all interfaces and superclasses in each concrete table.
<br/>

## Building the Mapping
1. When you are doing the schema yourself and if the domain logic is moderate to complex you can use a Transaction Script or Table Module design. In this case you can design the db around the data using classic db design techniques and use a RDG or a TDG to pull the sql away from the domain logic.
2. If you're using a Domain Model, then build your Domain Model w/o regard to the db in order to simplify the domain logic and treat the db design as a way of persisting the object's data. And in this case you might consider an Data Mapper or an Active record.
3. Building the model first is a good approach but this should be done only in short-iterative cycles. Don't do domain modelling for 6 months and then create the db, if any performance issues crop up here then refactoring will be very costly.
4. And in cases where the schema already exists, and if the domain logic is simple, you can use RDG or TDG classes that mimic the db and layer domain logic on top of this.
4a. And if the domain logic is complex then you will need a Domain Model which is highly unlikely to match the db design hence gradually build up the Domain Model and use Data Mappers to persist the data to the existing db.
<br/>

# OBJECT-RELATIONAL METADATA MAPPING PATTERNS
1. Metadata Mapping, Query Object, and Repository.
<br/>

## Metadata Mapping
1. This is about putting down all the mappings in a metadata file that details how columns in the db table map to the fields of an object.
2. Commercial O/R tool use a metadata mapping file.
3. These mappings can be used by the generic code to perform reading, updating and inserting the data.
4. the Hibernate mapping file is an example of this.
<br/>

## Query Object
1. A Query Object allows developers to build queries in terms of in-memory objects and data in such a way that the dev. need not know either SQL or the details of the relational schema.
2. The Query Object can then use Metadata Mapping to convert the object based expressions into appropriate sql expressions.
<br/>

## Repository
1. A system w/ a complex domain model benefits from a layer such as the one provided by the Data Mapper which isolates domain objects from the details of the db access code.
2. In such systems it can be worthwhile to build another layer of abstraction over the mapping layer where query construction code is concentrated.
3. This is useful when there are a large no.of domain classes or heavy querying.
4. And this layer helps minimize duplicate query logic.
5. A Repository basically mediates b/w the domain and data mapping layers, acting like an in-memory domain object collection.
6. Client objects constructs query specs declaratively and submit to the rep. for satisfaction.
7. Objects can be added to or removed from the repository, as they can from a simple collection of objects, and the mapping code encapsulated by the rep. will carry out the appropriate operations behind the scene.
8. This concept is more famous in Domain-Drive Design.
<br/>

## Database Connections
1. Queries to the db return a Record Set.
2. Disconnected Record Sets are those which can be manipulated even after the connection to the db is closed.
3. Connected Recrd Sets can be only be manipulated until the connection is open.
4. Connection creation is an expensive process hence connection pooling comes to the rescue.
5. When you need a connection fetch it from the pool and once done, release it back to the pool for someone else to use.
6. Since connections are mostly tied to transactions, a good way to manage them is to tie them to a transaction. Let the transaction deal w/ the connection so that you can only focus on the transaction.
7. You know when to begin the transaction and the trannsaction will open/fetch the connection and once you close the transaction (which you know when to), the connection will be closed by the transaction or release it to the pool.
8. If you are doing things outside of your transaction then you can fetch your connections straight from the pool and release them back later.
<br/>

## Misc Points
1. If you are using TDG, use column name indices as the result set returned is used by code that runs find operations on the gateway.
2. Its worth having simple test cases for crud operations for each db mapping structure, this will help you find out when your sql gets out-of-synch w/ the code.
3. Its always better to use static SQL that is precompiled than using Dynamic SQL.
4. Avoid using string concatenations while forming SQL queries.
5. Batching multiple SQL queries in a singel db call is also a better way for performance.
<br/>

# WEB PRESETATION PATTERNS
1. Basically 2 mains forms of structuring a program on a web server: scripts and server pages.
2. A CGI Script or a Servlet is an example of a Script but writing HTML in these becomes very difficult.
3. JSP, PHP and ASP are examples of server pages. HTML and processing logic both can be embedded in the server page.
4. Server pages works well for little processing tasks. Things get a lot more messy when many decisions are to be made based on the i/p.
5. Because the script style works best for interpreting a request and server page style works best for formatting a response, the obvious option was to use script for request int. and server page for resp. formatting.
6. This separation lead to the formation of Model View Controller pattern.
7. You can consider the controller in the MVC as an input controller.
8. The view and controller in the mvc have their own patterns.
9. All the patterns that you will come across here are: MVC, Page Controller, Front Controller, Application Controller, Template View, Transform View and Two-Step View.
<br/>

## Model View Controller
1. Let's refer the Controller in the MVC as an Input Controller.
2. In an MVC, the request comes in to an input controller, which pulls off information from the request, forwards the business logic to the appropriate model object. 
3. The model object talks to the data source and does what is asked in the request and gathers information for the response, when done control is transferred back to the input controller w/ the information gathered. 
4. The i/p controller looks at the results and decides which view is needed to display the response and then passes control to the view along w/ the response data.
5. Primary reason to apply MVC is to totally separate Models from the View i.e. the Web presentation, thereby making modifications to presentations easier w/o any cascading effects.
<br/>

## Application Controller
1. The purpose of AC is to handle flow of the application, deciding which screens to appear in which order.
2. AC can be part of the presentation layer or as a separate layer b/w the presentation and the domain.
3. AC can be written independent of the presentation.
4. If your app. has a lot of logic around which screens to display when and the navigation around them then ACs are useful. Or If the mapping b/w the pages and the actions on the domain is complex, then also ACs are useful.
5. Bottom line is, If the machine is in control of the screen flow, you need an AC. If the user is in control of the screen flow, then you dont need an AC.
<br/>

## Page Controller
1. This is an i/p controller pattern.
2. Here the idea is to have one i/p controller for each page.
3. This can be also be modified to have one i/p controller for each action like a button click or a link click.
<br/>

## Front Controller
1. This is also an i/p controller pattern.
2. W/ any i/p controller there are 2 responsibilities - handling the HTTP request and deciding what to do w/ it.
3. In a FC, only one object handles all requests. 
4. The single handler interprets the URL to figure what kind of request it's dealing w/, carries out common behavior and the dispatches to command objects for behavior specific to the request.
<br/>

## Template View
1. This is a View pattern.
2. TeV basically allows you to write presentation logic in the structure of the page alongside w/ any dynamic content that you wish to write.
3. That means, both the presentation logic and any other programming/domain logic can also be written in the same page.
4. Server pages like JSP, PHP and ASP are examples of this.
5. Provides flexibility but not a practical way for real enterprise applications. Makes code messy and unreadable.
<br/>

## Transform View
1. This is also a View Pattern.
2. TrV is very useful if you are working w/ domain data that is in XML format or can easily be converted to it.
3. XSLT is an example of TrV.
4. An i/p controller picks the appropriate XSLT stylesheet and applies it to the XML obtained from the model.
<br/>

## Two-Step View
1. This is also a View Pattern.
2. In a single-stage view, there will be one view component for each screen in the application.
3. The view takes the domain data and renders it in html.
4. In a two-stage view, there is one first-stage view for each screen but only one second-stage view for the whole application.
5. This makes global changes to HTML easy since there is only one object to make changes to alter every screen on the site.
6. This is also useful when you have a Web app whose services are used by multiple front-end customers like a airline reservation system. Multiple airlines maybe using the same system hence they can inherit the same second-stage view and apply their own first-stage view on top of it.
7. Can also be used to output to different types of devices. Sharing the same logical view but w/ different first-stage view.
<br/>

## Concurrency
1. The reason because of which enterprise app developers can get away w/ a naive understanding of concurrency is because of the Transaction Managers.
2. Transactions provide a framework that help us avoid most of the tricky aspects of concurrency.
3. But we still have to manage concurrency for data that spans transactions.
<br/>

## Offline concurrency
1. Concurrency control for data that is manipulated during multiple transactions.
<br/>

## Lost Updates
1. Let's say A and B are going to work on the same file on different methods.
2. A edits the file first and a moment later B also starts editing the file and B finishes before A and saves the file.
3. Now when A first started editing the file, he dint have the changes made by B and when he saves his changes all of B's updates will be lost.
<br/>

## Request
1. This corresponds to a single call from the outside world which the application is currently working on and might optionally send a response as well.
<br/>

## Session
1. It is a long-running interaction b/w Client and Server.
2. It may consist of a single request or multiple requests.
3. Commonly session begins when the user logs in and lives through his interactions w/ the application and ends when he logs out.
<br/>

## Thread
1. A light-weight active agent within a single process.
2. Threads can support multiple requests within a single process.
3. Threads share memory and such sharing leads to concurrency issues.
<br/>

## Process
1. A process is a heavy-weight execution context which usually provides a lot of isolation for the internal data it works on.
<br/>

## Transactions
1. Several requests/interactions usually b/w an application and a db.
<br/>

## Immutable Data
1. The whole problem of concurrency occurs only when the data you are sharing can be modified.
2. This does not arise w/ immutable data since it cant be modified.
3. Ofcourse cant make the entire data as immutable since the whole point of an application is to modify data but having as much as possible immutable data is best.
<br/>

## Optimistic Locking
1. Taking the example of a source code control system.
2. If A and B want to edit the same file.
3. Both A and B can check out the file.
4. Let's say B will make changes first and commits it, nothing happens, changes gets saved.
5. When A is about to commit his changes then the optimistic locking gets kicked in and rejects the commit. Now its for A to figure out the change and merge the changes accordingly.
6. That is here, multiple people can edit the same file at the same time and locking mechanism gets kicked in only when commiting changes.
7. This is about conflict detection.
<br/>

## Pessimistic Locking
1. In this, whoever checks out the file first will prevent others to check out until it is not comitted.
2. That is here, only one person can work on one file at a time.
3. This is about conflict prevention.
<br/>

## ACID
1. Atomicity: All or nothing. All changes done within an transaction must completely commit or fully roll back, no half-baked work.
2. Consistency: All resources of the system must be in a consistent, non-corrupt state at the start and completion of a transaction.
3. Isolation: The result of one transaction must not be visible any other open transaction until that transaction commits successfully.
4. Durability: Any result of a committed transaction must be permanent, basically means, that data must survive any crash.
<br/>

## Long Transaction
1. Transactions should generally be kept as short as possible and not span across multiple requests.
2. A transaction that spans multiple requests is known as LT.
<br/>









