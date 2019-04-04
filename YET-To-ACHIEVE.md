## lazy loading
1. in case of multiple collections (esp Lists w/ eager loading), hibernate throws MultipleBagFetchException, to overcome this I used Fetch.SUBSELECT.
2. Ideal solution is to perform lazy loading but in order to do this I need to use hibernate sessions, which I couldn't achieve.
3. check this : https://grokonez.com/hibernate/use-hibernate-lazy-fetch-eager-fetch-type-spring-boot-mysql

## caching
1. I din't explicitly use any cache, though I am not sure if spring boot uses something by default.
2. I guess there are multiple cache levels (like second level cache), I din't use any.
3. Don't know how much of a performance difference these make.

## spring security
1. Coudln't integrate spring security into theVault application.
2. The application became too big before I could integrate it so I din't.

## spring validator
1. was not able to do field level validations for nested objects because I was not able to refer the nested object in the view.
2. in some cases, i couldn't do it because the object being loaded in the model was different from what was required in the validator to perform spring validation.
3. good reference post for validation: https://stackoverflow.com/questions/12146298/spring-mvc-how-to-perform-validation
4. a decent example of spring validator: https://www.journaldev.com/2668/spring-validation-example-mvc-validator

## performance
1. din't measure the performance of spring data jpa vs native queries.
2. as of now i don't know which one is better when.
3. also dint check how these approaches behave and how to solve as the application scales to some 10k, 50k and 100k users.
4. spring boot actuator is also something which comes with default metric tools for use in prod, din't use it, don't know what it exactly is.

## pagination
1. there is some pagination feature in spring data jpa but i dint implement.
2. it should be much needed feature, should see what it does and how does it work.

## exception handling
1. dint implement any exception handling in theVault application.and this is one of the basic things.
2. good ref. post for exception handling in spring: https://stackoverflow.com/questions/12660262/spring-mvc-hibernate-data-validation-strategies/12661291#12661291

## tdd
1. did unit testing and db level integration testing but din't do tdd.
2. even unit and integration testing was done sparsely, probably tdd will give more test coverage.
3. used this as reference: http://www.springboottutorial.com/spring-boot-unit-testing-and-mocking-with-mockito-and-junit

## deploying war/jar
1. theVault was run from the application directly which is not how applications are run in prod.
2. have to know how to make a jar/war and deploy and run a spring boot app.

## Java 8 features
1. din't use much of java 8 features like functional programming, lambdas, streams, optional etc.
2. want to use them and also measure and document the performance difference against traditional java programming.

## Code Review Tools
1. din't use any code review tools.
2. this is also pretty important to know good practices.
3. want to focus cyclomatic complexity analysis tools.
 
