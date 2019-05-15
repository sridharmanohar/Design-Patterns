## Spring Boot Test Starter brings in a wide range of dependencies for Unit Testing
1. Basic Test Framework - JUnit
2. Mocking - Mockito
3. Assertion - AssertJ, Hamcrest
4. Spring Unit Test Framework - Spring Test: <br/>
   a. Contains server-side support for testing Spring MVC applications.<br/>
   b. org.springframework.test.web.servlet.request: Contains built-in RequestBuilder implementations.<br/>
   c. org.springframework.test.web.servlet.result: Contains built-in ResultMatcher and ResultHandler implementations.<br/>

## @WebMvcTest vs @DataJpaTest
1. Both these annots. are part of spring boot test package.
2. @WebMvcTest is used for testing the mvc part.
3. @DataJpaTest is used for testing your service layer i.e. connections to db.
4. Both these annots. will not work together, hence, you will have to separate your mvc layer test from the service layer ones.
5. @DataJpaTest will by default use an in-memory db for all the tests. You have to specify you db config. in application.properties file in resources folder.
6. By default, all @DataJpaTest are @Transactional i.e. they will roll-back once done. You can also explicitly mention the test w/ an @Transactional annot.

