
## Relationships
1. Bi-dir One-to-One<br/>
   a. Example: Two entities - Employee and Cubicle.<br/>
   b. Entity Employee references a single instance of Entity Cubicle.<br/>
   c. Entity Cubicle references a single instance of Entity Employee.<br/>
   d. Employee is the owner of this rel.<br/>
   e. Employee is mapped to table EMPLOYEE.<br/>
   f. Cubicle is mapped to table CUBICLE.<br/>
   g. EMPLOYEE tab contains a fk to CUBICLE.<br/>
2. Bi-dir Many-to-One/One-to-Many <br/>
   a. Example:Two entities - Employee and Department .<br/>
   b. Entity Employee references a single instance of Entity Department.<br/>
   c. Entity Department references a collection of Entity Employee.<br/>
   d. Entity Employee is the owner of the relationship.   <br/>
   e. Employee is mapped to table EMPLOYEE.<br/>
   f. Department is mapped to tab. DEPARTMENT.<br/>
   g. EMPLOYEE tab contains a fk of DEPARTMENT.<br/>
3. Uni-dir One-to-One<br/>
   a. Example: Two entities: Employee and TravelProfile<br/>
   b. Entity Employee references a single instance of Entity TravelProfile.<br/>
   c. Entity TravelProfile does not reference Entity Employee.<br/>
   d. Employee is the owner of this rel.<br/>
   e. Employee is mapped to tab EMPLOYEE.<br/>
   f. TravelProfile is mapped to tab TRAVELPROFILE.<br/>
   g. EMPLOYEE tab has a fk to TRAVELPROFILE.<br/>
4. Uni-dir Many-to-One <br/>
   a. Example: Two entities: Employee and Address.<br/>
   b. Entity Employee references a single instance of Entity Address.<br/>
   c. Entity Address does not reference Entity Employee.<br/>
   d. Entity Employee is the owner of the relationship.<br/>
   e. Employee is mapped to tab EMPLOYEE.<br/>
   f. Address is mapped to tab ADDRESS.<br/>
   g. EMPLOYEE contains a fk to ADDRESS.<br/>
5. Bi-dir Many-to-Many <br/>
   a. Example: Two entities: Project and Employee.<br/>
   b. Entity Project references a collection of Entity Employee.<br/>
   c. Entity Employee references a collection of Entity Project.<br/>
   d. Entity Project is the owner of the relationship.<br/>
   e. Project is mapped to tab PROJECT.<br/>
   f. Employee is mapped to tab EMPLOYEE.<br/>
   g. Join table PROJECT_EMPLOYEE has two fk cols each belonging to PROJECT and EMPLOYEE.<br/>
6. Uni-dir one-to-Many <br/>
   a. Example: Two entities: Employee and AnnualReview.<br/>
   b. Entity Employee references a collection of Entity AnnualReview.<br/>
   c. Entity AnnualReview does not reference Entity Employee.<br/>
   d. Entity Employee is the owner of the relationship.<br/>
   e. Employee is mapped to tab EMPLOYEE.<br/>
   f. AnnualReview is mapped to tab ANNUALREVIEW.<br/>
   g. Join tab. EMPLOYEE_ANNUALREVIEW has 2 fk cols each belonging to EMPLOYEE and ANNUALREVIEW.<br/>
7. Uni-dir Many-to-Many <br/>
   a. Example: Two entities: Employee and Patent.<br/>
   b. Entity Employee references a collection of Entity Patent.<br/>
   c. Entity Patent does not reference Entity Employee.<br/>
   d. Entity Employee is the owner of the relationship.<br/>
   e. Employee is mapped to tab EMPLOYEE.<br/>
   f. Patent is mapped to tab PATENT.<br/>
   g. Join tab EMPLOYEE_PATENT has 2 fk cols each belonging to EMPLOYEE and PATENT.<br/>

## @Autowired
1. This is used by Spring to inject dependencies.
2. This can be used on a constructor, setter or a property.
3. For e.g., If you have a class and there are not setters for it, just add the instance of this class (in the class where it is required) like private <Classname> <varname>; and annotate it with this annotation and this class instance will be available.
4. Similarly, you can annotate a constructor w/ this. Like:<br/>
   class SomeClass {<br/>
      private SomeRepo someRepo;<br/>
      <br/>
      @Autowired   <br/>
      public SomeClass(SomeRepo someRepo) {<br/>
         this.someRepo = someRep;<br/>
      }<br/>
    }<br/>
    This will inject the required  repo instance.<br/>

## @Bean
1. This tells spring that this particular bean has to managed by the spring container.

## @SpringBootApplication
1. This indicates a config. class that declares @Bean methods and triggers auto-config and component scanning.
2. This one annotation is equivalent to @Configuration, @EnableAutoConfiguration and @ComponentScan annotations.

## @Entity
1. This is a JPA annotation.
2. Basically means a class can be mapped to a table.

## @GeneratedValue
1. This is a JPA annot.
2. When using mysql always use IDENTITY as your generation strategy because in mysql there is no direct concept of sequences  (mysql has auto_increment), so because of which when you set it to AUTO it looks for the hibernate_sequence which it
will not find and throw an error, hence use IDENTITY.

## @Column
1. If the name of the field/property in your bean is in camelCase then Spring will automatically convert that into snake_case.
2. And, if you db col name is not in snake_case then there will be an obvious mismatch and an error will be thrown during
query execution.
3. To avoid this, you can use the name attr of the annot. and specify the name that you want spring to use.

## @Size
1. You can use this annot. to specify the min/max size of the field and spring will take care of the validations.

## @NotNull
1. Valid as long as it is not null, but can be empty.

## @NotEmpty
1. Valid as long as it is not null and size/length is greater than zero.

## @Transient
1. If you do not want to persist any field of an entity then use this annot. to tell JPA that this particular should not
be persisted.

## @Controller
1. This is a spring annot.
2. This is to mark a class as a Spring MVC Controller.
3. The job of the controller is to build a model object and find a view.

## @RestController
1. This is added in Spring 4.
2. This is a special case of @Controller.
3. This simply returns the object to the HTTP Response as an JSON/XML. or as a normal string.
4. If we want to achieve this functionality but not use this annot. then we can use @Controller with @ResponseBody annot.
to achieve the same.

## @GetMapping
1. This is a special case of @RequestMapping.
2. This is same as @RequestMapping(method=GET).
3. Similarly, there are other special mappings like @PutMapping, @DeleteMapping and @PostMapping.
4. All these are for mapping web requests onto methods.

## Query creation using Spring Data Repositories
1. This allows us to query db by just mentioning the method names which have to follow a certain nomenclature.
2. For e.g. For the entity User having properties firstname, lastname, username, password, doj etc.
3. If you want to query a user/list of users on the basis of their firstname then simply create an interface by extending the Repository interface (pass in the entity name along with its primary key type).
4. And, then write a method as : User findByUsername(String name).
5. The prefix's like findBy, readBy, queryBy, countBy, getBy will be stripped by Spring and then it will look for a field by the name username in the entity (case matters).
6. If in the above case, you mention, findByUserName then Spring will look for a field naming userName in the entity.
7. Many keywords like And, Or etc are also supported. For complete list look at Spring Data JPA ref. doc.

## @Query
1. This belongs to spring data jpa.
2. This allows us to mention the query ourself still using object domain model.
3. Alternatively, if you want to mention a native sql query then you can use the nativeQuery=true attr of this annot. and mention the query in native sql.

## CommandLineRunner
1. If you implement this interface then you will have to override it's run method.
2. And whatever you mention in that run method will be called as soon as the spring boot application is up.
3. So, If you want to configure a few things like logs etc, can be put in this method.
4. Generally not required to be done.

## RestTemplate
1. This is part of Spring Web Client package and is for consuming REST web services.
2. getForObject method of this class can make a RESTful web service call to the given endpoint and consume data which is offloaded into the desired object.

## @JsonIgnoreProperties
1. The is from jackson package.
2. The ignoreUnknown=true attr of this annot. will help you ignore all those properties of the json (while de-serializing) which you do not want to hanlde and there is not match for them in your pojo.
3. It is of no use if all your bean setters are a match to the json props.

## @JsonAlias
1. This is useful if you pojo field name is not a match with the json prop. name.
2. You can then provide an alias name for your pojo field name which is a match to the json prop.
3. Actually, jackson while de-serialization looks for a matching setter (not for the field) in the pojo and as long as your setter name is a match w/ the json prop., there is no problem.

## @ManyToMany
1. This belongs to javax persistence (jpa) package.
2. In hibernate, by default, whenever you are trying to load a collection the fetch type is set to LAZY and this will lead to an error if you are not using hibernate session (spring uses EntityManager of its own).
3. So when not using hibernate sessions w/ spring and if you have collections in your entities then explicitly set the fetchtype to eager.
5. This is an attr. of this annot.

## @JoinTable
1. This is also part of jpa (javax persistence).
2. This is for letting your jpa provider know which join tables to look for while querying for data.
3. That is, say, you have 2 entities: Employee (mapped to EMPLOYEE table) and Projects (mapped to PROJECTS tab.) and then there is a third table EMPLOYEE_PROJECTS (which contains pk's of EMPLOYEE and PROJECTS tab.), and this third table is not an entity, so to let your jpa provider of this third impo. tab. which is not an entity in your app, use @JoinTable and its attrs.

## Spring Data
1. This is one of the projects in Spring family and this is an umbrella project.
2. The main purpose of this is to make it easy to access different relataion, non-relational databases, map reduce frmaeworks and cloud-based data services.
3. This umbrella project contains many sub-projects related to specific db.
4. Some of the sub-projects under this are Spring Data JDBC, Spring Data LDAP, Spring Data MongoDB etc.

## Spring Data JPA
1. This is a sub-project under the Spring Data project.
2. This is kind of a library which helps dealing with JPA easier.
3. Some of its features are pagination support, @Query annot. etc.
4. You still have to use an JPA implementation like hibernate even when using Spring Data JPA.

## MultipleBagFetchException
1. You encounter this when one or more of entities have more than one collection association.
2. Say, an entity User has two collections being loaded with @OneToMany and @ManyToMany (two Lists<>), then hibernate throws this exception.
3. And, as far as I know, this also happens only when the fetch option is eager, I think, not sure though.
4. Way to get around this is to use Set instead of Collection/Set.

## @PathVariable
1. This is part of Spring web annot.
2. This is to map a method param to an incoming request param.

## @Valid
1. Part of JPA validation package.
2. This enables the validations done by using JPA annot. such as @NotNull, @Size, @NotEmpty on the pojos to be available in the front-end like thymeleaf.
3. Say, if there is a empty validation violation, then the error message that is generated is passwd back to the view for it access and display it on the screen.
4. If you do not use this, validation will still happen but the error message wont appear on the screen and hence the transaction fails with the stack trace.
5. This is useful only when you are using the jpa validation annot.

## BindingResult
1. This is part of spring's validation package.
2. This has to follow the object that is being validated otherwise this wont work.
3. That is, in the method param, this has to be exactly after the object (with a @Valid) annot.
4. This acts as a data binder holding the results of the validations performed.
5. If you dont put this after the model being validated then you will get this error:
'An Errors/BindingResult argument is expected to be declared immediately after the model attribute'
6. And, if you don't use this at all, then the validation happens but binding the result of the validation will happen and that will throw an error.
7. Bindingresult also has methods like reject (for global errors - not related to one field but related to the whole object) and rejectValue (with an option to pass custom error message) - basically this acts the validation result holder and passes the data to the view for it to render
## ValidationMessages.properties
1. This is the property file which hibernate (or any jpa provider for that matter) will look for when providing error messages for the validations done using jpa validation annot.
2. So to override the default error messages, you can use the message attr. of the jpa validation annot. and provide a corresponding custom error message in a custom ValidationMessages.properties file.

## Model vs ModelMap vs ModelAndView
1. All these are holders for model attributes and helps in passing them to the views for them to render.
2. Model: this is from spring ui package.
3. This is actually an interface.
4. ModelMap: this is nothing but an extension of LinkedHashMap. 
5. That means, this is ordered and maintains an insertion order but hence at the same time it will take more memory compared to an HashMap.
6. The LinkedHashMap uses a doubly linked-list to keep track of insertions and hence this will take more memory compared to HashMap.
7. ModelMap is not bound to spring mvc but still does the same task of rendering views.
8. ModelAndView is from the spring web servlet package.
9. This is for holding both Model and the view name, din't find it much useful it except for the fact that you can put the view name in its constructore itself (instead as a return string).

## @Validated
1. This is part of spring validation package.
2. Use this to annotate the class/object that is being validated using spring validator.

## Bean validation vs Spring validator
1. Bean validation means using the javax annot. on the bean fields such as @NotEmpty, @NotNull, @Size etc. which are then automatically validated by the jpa provider (hibernate - using hibernate validator).
2. When you use Spring validator you do not use those javax annot. and rather create a separate class for by implementing the Validator interface and override it's supports and validate methods.
3. Spring validator gives you more control for complex validations such as applying some logic on the validation like age<10 and age>20 or in the range of x to x, something like that.
4. If you use Spring validator, use @Validated otherwise @Valid in the controller.
5. For Spring Validator, you need to DI it's instance in the controller.
6. Spring Validator also binds its errors to the BindingResult class.
7. Both these are not mutually exclusive, so can be used together.
8. But, both of these are only for UI level validations i.e. to perform validations on what user has entered on the screen, not for other business logic.

## Autowiring fails with a NoSuchBeanDefinitionException, following could be the reasons:
1. when the qualifying has bean not been annot. w/ @Component or @Controller or any another stereotype annot.
2. if you autowired an interface then you must use a @Qualifier to let spring specificially know which implementation of that interface has to be wired.

## @Qualifier
1. This takes a string and that is actually used to specify the name of the qualifying bean that needs to be autowired.
2. Used especially when you are autowiring an interface and since an interface can have multiple implementations, it becomes necessary to explicitly mention the name of the qualifying bean/implementation which we want to be auto-wired.

## Stereotype Annot.
1. @Component, @@Controller, @Indexed, @Repository, @Service - these are the stereotype annot.
2. These annot. basically are for auto-detection and classpath scanning.
3. If you autowire a bean then the qualifying bean has to annot. w/ one of these sterotype annot. for spring to pick them up otherwise a NoSuchBeanDefinitionException will be thrown.
4. Basically, @Component is the base stereotype annot. and all others mentioned above are special cases of that but more or less anything will do the same.

## @InitBinder
1. This annot. is used on a method and its purpose is to customize request parameters, template uri variable and backing/command objects.
2. command/backing objects are nothing but pojos/entities.
3. This annot. is basically used on a method inside a controller.
4. Methods annot. with support all arguments types that handler methods support and WebDataBinder is one of them. Command objects are not supported.
5. The methods annot. w/ this are called in every HTTP request if the 'value' attr is not mentioned.
6. To be more specific about which objects this applies to, mention the value attr. Value takes single/multiple names of command/request attrbs.
7. There is no limitation to how many methods w/ this annot. can be.
8 Not sure yet, but mostly, it looks like the 'value' for this should be same as what you set in the model attr.

## WebDataBinder
1. This extends DataBinder.
2. This is used to register custom formatters, validators and propertyeditors.
3. Basically, this is for binding request params to java bean objects.
4. Whenever you are using this it is highly recommended to mentioned the allowedFields otheriwse there is a security risk because in case of an http post form submittion, a malicious client can attempt to send an application by spplying values for fields that do not exist.

## DataBinder setAllowedFields
1. Register fields that should be allowed for binding.
2. Default is all fields.
3. Restrict this for example to avoid unwanted modifications by malicious users when binding HTTP request parameters.
4. HIGHLY IMPORTANT - SECURITY RISK.
5. or use setDisallowedFields : which is to register fields that should not be allowed for binding. mark fields as disallowed to avoid unwanted modifications by malicious users when binding http req params. 
6. If you disallow all fields then there will be nothing for data binding and might throw an error: 
2019-03-14 14:02:28.497 DEBUG 17085 --- [nio-8080-exec-3] o.springframework.validation.DataBinder  : Field [lastname] has been removed from PropertyValues and will not be bound, because it has not been found in the list of allowed fields

## Things to take care while doing DDL (insert, update, delete)
1. You need to make sure the method (performing the ddl) is annotated with @Transactional and @Modifying annot.
2. @Transactional can be done at class level also but @Modifying is method level.
3. @Transactional is available in both jpa api and spring transaction api. You can use any.
4. @Modifying is in springs data jpa.
5. If you don't use these you'll get errors like:
org.hibernate.hql.internal.QueryExecutionRequestException: Not supported for DML operations
Executing an update/delete query; nested exception is javax.persistence.TransactionRequiredException
6. Btw, these are only required if you are either using a jpa query or a native sql query. Not required when using spring data jpa.

## Cascade ALL
1. If you do not use this, then cascading updates/insertions will not happen.

## Spring Boot Test Starter brings in a wide range of dependencies for Unit Testing
1. Basic Test Framework - JUnit
2. Mocking - Mockito
3. Assertion - AssertJ, Hamcrest
4. Spring Unit Test Framework - Spring Test: 
   a. Contains server-side support for testing Spring MVC applications.
   b. org.springframework.test.web.servlet.request: Contains built-in RequestBuilder implementations.
   c. org.springframework.test.web.servlet.result: Contains built-in ResultMatcher and ResultHandler implementations.
