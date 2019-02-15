
# CREATIONAL PATTERNS
1. These patterns deal with class instantiation/ object creation process.
2. People often use Factory method pattern to create objects.
3. Designs using Asbtract factory, Prototype and Builder are more flexible compared to Factory method and also more complex.
4. Often, designs start w/ factory method pattern and then evolve towards other design patterns as more flexibility is required.
<br/>

## Singleton Pattern
1. A class can be instantiated only once.
2. In terms of java, a class can be instantiated only once per jvm.
3. A Singleton can be created in the following ways:<br/>
   a. Using a public static final field which return the instance.<br/>
   b. Using Lazy Initialization: This will create the instance only when asked for; the first time.<br/>
   c. Early Initialization: <br/>
	    i. This will create the instance as soon as the class loads.<br/>
	   ii. This is also known as public static factory method approach.<br/>
   d. Enum: This functionally is equivalent to a public field approach.<br/>
4. The problem with public static final field and early initialization is that the singleton instance is created as soon as the class loads, whether there is any demand for the or not.
5. In case of Lazy Initialization, the instance is created only when the demand arises.
6. The thing with enum singleton is that there is no use of constructors here which was the case with lazy and early initializations.
<br/>

## Factory Method Pattern
1. It is a class creational pattern.
2. Super class can be either an interface or an abstract class.
3. A factory class creates the required sub-class instance based on the inputs.
4. This promotes loose-coupling.
5. Only the factory class is exposed to the Client.
6. This is actually called as Factory method pattern because it's the method in the factory class which returns the desired instances.
7. Use this pattern when:<br/>
   a. you have a super class and multiple implementations of it and based on the input you need to return one of the sub-classes.<br/>
   b. a class can't anticipate which class of objects it must create.<br/>
8. Factory method pattern encourages coding to interface rather than to implementation, hence loose-coupling.
9. Participants:<br/>
   a. An abstract class/interface.<br/>
   b. sub-classes that extend or implement the abstract class/interface.<br/>
   c. A factory class with a static method which returns the desired instance of the sub-class depending upon the input.<br/>
   <br/>

## Abstract Factory Pattern
1. This is a object-scoped creational design pattern.
2. This is basically useful when creating families of related or dependent objects w/o specifying their concrete classes.
3. As in the case of factory method, there is a single factory class which returns different sub-classes based on the inputs, here, there will one factory class for each sub-class. And an abstract factory class will return the object of the desired sub-class based on the input factory class.
4. This is basically factory of factories.
5. Abstract factory provides abstraction for factories of concrete classes whereas factory method pattern provides abstraction for concrete classes.
6. No if-else or switch cases in the factory class (which was the case with factory method pattern). This is better especially when there are a lot of sub-classes,
then providing switch or if-else in the single factory class won't be a good method, hence in that case having one factory for each sub-class is better.
7. One disadvantage I see here is that there is some redundancy i.e. each subclass has a factory class that means any changes in the subclass will lead to changes
in its corresponding factory class.
8. But this probably a cleaner design when there are a lot of subclasses implementing the interface/abstract class. Then this is probably a better object creation
mechanism.
9. Participants:<br/>
   a. An abstract class/interface.<br/>
   b. sub-classes that extend or implement the interface.<br/>
   c. An AbstractFactory interface that provides a abstract method which returns an instance of the main interface/abstract class.<br/>
   d. One factory class for every subclass. This factory class will implement the AbstractFactory interface.<br/>
   e. A factory class with a static method (which is accessed by the client) which returns an instance of the main interface/abstract class by calling the abstract method of AbstractFactory interface.<br/>
   <br/>
   
## Builder Pattern
1. This is an object-scoped creational pattern.
2. Dependency Injection may be less supported.
3. Use Builder Pattern when the situation has the following:
4. Complex Constructor: Multiple constructors with multiple combination of params. And it becomes increasingly confusing when there are many params with same data type and then passing these params through the const becomes confusing because we do not know which param are we actually passing.
5. Large number of params: Having many params and with some required and some optional.
6. The opposite of Builder pattern is the Telescoping pattern where multiple const. with varying params are written.
7. This pattern comes handy especially when you have large no.of params out of which a good no.of params are optional.
8. In case of multiple optional params, we can also have a single constructor with only mandatory params and setters for other optional params (also known as JavaBeans pattern) but then this might lead to object being in inconsistent state. Builder pattern solves the problem of having the object in an inconsistent state.
9. Participants of Builder pattern:
10. Main product class with all its mandatory and optional fields. A private const. with all fields. Private cosnt. is to ensure that the only way this class is instantiated is through the Builder class and Getters for all fields.
11. A static builder class with a copy of all fields as in the main product class. A public const. w/ mandatory params and setters for all other optional params. returning the same builder object (hence avoiding inconsistent state).
12. Disadvantage:
13. Redundant code.
14. Any changes in concrete class will require changes in the builder class also, esp. when the change is related to the fields/variables.
15. This pattern was introduced to solve some of the problems associated with Factory and Abstract Factory when the object contains a lot of attributes.
16. The problem with Factory method pattern in this case is there is no option to send only the few required params hence all params will have to be sent by the client while creating/requesting for the desired object and for optionals NULL value must be present, hence factory method pattern is not preferred in this scenario.
<br/>

# STRUCTRAL PATTERNS
1. These patterns provide different ways to create a class structure.
<br/>

## Adapter Pattern
1. The main purpose of this to make two incompatible interfaces work together. The thing that joins these two incompatible interfaces is the adapter.
2. Consider Adapter pattern with an example of a mobile charger. The input voltage from the socket is 240V but the mobile can take in 3V, here comes the mobile charger which acts as an adapter b/w the input socket and the mobile.
3. Adpater pattern can be implemented using class based and object based approaches. In the class based approach, the pattern uses inheritance whereas in the Object based approach it makes use of composition.
4. This is probably ore useful when you as client are making of two APIs.
5. Adapter is generally used when you come across two incompatible classes that need to work together.
<br/>

## Proxy Pattern
1. Proxy pattern provides proxies or placeholders to an object mainly to control or limit access to the object in question.
2. For instance, let's say there is a class which executes some commands on the server and you want to limit access to this class methods only to admins then a proxy pattern can be used.
3. Proxy pattern can be used to separate the access control logic from the class that needs to implement business logic. This leads to Single Responsibility Principle.
4. Proxies control access to an object.
<br/>

## Facade Pattern
1. The main intent of this pattern is to hide the complex chunk of code and provide a simpler API for usage.
2. The difference factory and facade is that: <br/>
2a. factory deals with object creation by hiding implementation details and facade deals with providing a simple higher level api for usage.<br/>
2b. factory can return a different object everytime depending on the input whereas facade will return the same object but it makes ths api simpler to use.<br/>
3. The facade is probably more useful when you are designing API for the client to use.
4. Difference between Facade and Adapter:<br/>
4a. Facade promotes creating a new interface to resolve the complexity and make the usage ease whereas Adapter makes use of the existing interfaces.<br/>
4b. Adapter opposes the creation of a new interface to solve the problem it is trying to solve.<br/>
<br/>

## Bridge Pattern
1. Bridge pattern basically provides a bridge between two set of interface hierarchies where one is dependent on the other for some functionality.
2. For example, let's consider a Missile interface which has types of missiles as its implementations and consider a Igniter interface which has different kinds of igniting techniques as its implementations. For the missile to take off it needs to be ignited, so the Missile implementations depend on the particular type of Ignitor to ignite the missile. Such problems are solved by Bridge design pattern.
3. This pattern uses object composition to solve such problems.
4. This pattern differs with Adapter pattern in thw following ways:<br/>
4a. Adapter focuses on resolving the incompatabilities between two existing interfaces.<br/>
4b. Adapter makes two independently designed classes to work together.<br/>
4c. Bridge provides a bridge between two implementations where one is dependent on the other for some work.<br/>
<br/>

# BEHAVIORAL PATTERNS
1. These patterns identify communication patterns between objects and assign responsibilities to objects.
<br/>

## Template Pattern
1. This pattern defines a skeleton of the algorithm and the implementation of certain steps is done by subclasses.
2. hence, in this pattern, we have method w/ concrete implementation and methods w/o any implementation.
3. This pattern is applicable to a problem where certain steps are common for all implementations and other steps will vary from implementation to implementation. And there is also a certain sequence in which these steps have to be executed.
4. This pattern uses inheritance.
<br/>

## Strategy Pattern
1. This pattern enables us to select an algorithm at runtime.
2. This pattern specifies behaviors as interfaces and these interfaces are implemented by specific classes. For e.g. A car has brake and accelerate functionalities, both these functionalities will be defined as interfaces and classes implement them.
3. This pattern is basically applicable when functionalities/functionality has different strategies.
4. Strategy pattern uses composition over inheritance.
<br/>
