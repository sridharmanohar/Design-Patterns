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

## tdd
1. did unit testing and db level integration testing but din't do tdd.
2. even unit and integration testing was done sparsely, probably tdd will give more test coverage.
3. used this as reference: http://www.springboottutorial.com/spring-boot-unit-testing-and-mocking-with-mockito-and-junit
4. Also din't work on Test coverage.  


