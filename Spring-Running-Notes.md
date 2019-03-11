
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
