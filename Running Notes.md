
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
