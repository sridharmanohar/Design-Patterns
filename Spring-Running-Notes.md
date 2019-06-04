1. **@Autowired**
    * This is used by Spring to inject dependencies.  
    * This can be used on a constructor, setter or a property.  
    * For e.g., If you have a class and there are no setters for it, just add the instance of this class (in the class where it is required) like private <Classname> <varname>; and annotate it with this annotation and this class instance will be available.  
    * Similarly, you can annotate a constructor w/ this. Like:  
          *class SomeClass {*  
          *private SomeRepo someRepo;*  
          <br/>
          *@Autowired*  
          *public SomeClass(SomeRepo someRepo) {*  
             *this.someRepo = someRep;*    
          *}*  
        *}*  
        * This will inject the required  repo instance.<br/>  

2. **@Bean**
    * This tells spring that this particular bean has to be managed by the spring container.  

3. **@SpringBootApplication**
    * This indicates a config. class that declares @Bean methods and triggers auto-config and component scanning.  **what is component scanning??**  
    * This one annotation is equivalent to @Configuration, @EnableAutoConfiguration and @ComponentScan annotations.  

4. **@Controller**
    * This is a spring annot.  
    * This is to mark a class as a Spring MVC Controller.  
    * The job of the controller is to build a model object and find a view.  

5. **@RestController**
    * This is added in Spring 4.  
    * This is a special case of @Controller.  
    * This simply returns the object to the HTTP Response as an JSON/XML. or as a normal string.  
    * If we want to achieve this functionality but not use this annot. then we can use @Controller with @ResponseBody annot. to achieve the same.  

6. **@GetMapping**
    * This is a special case of @RequestMapping.  
    * This is same as @RequestMapping(method=GET).  
    * Similarly, there are other special mappings like @PutMapping, @DeleteMapping and @PostMapping.  
    * All these are for mapping web requests onto methods. 

7. **CommandLineRunner** 
    * If you implement this interface then you will have to override it's run method.  
    * And whatever you mention in that run method will be called as soon as the spring boot application is up.  
    * So, If you want to configure a few things like logs etc, can be put in this method.  
    * Generally not required to be done.  

8. **RestTemplate**
    * This is part of Spring Web Client package and is for consuming REST web services.  
    * getForObject method of this class can make a RESTful web service call to the given endpoint and consume data which is offloaded into the desired object.  

9. **@JsonIgnoreProperties**
    * The is from jackson package.  
    * The ignoreUnknown=true attr of this annot. will help you ignore all those properties of the json (while de-serializing) which you do not want to hanlde and there is not match for them in your pojo.  
    * It is of no use if all your bean setters are a match to the json props.  

10. **@JsonAlias**
    * This is useful if you pojo field name is not a match with the json prop. name.  
    * You can then provide an alias name for your pojo field name which is a match to the json prop.  
    * Actually, jackson while de-serialization looks for a matching setter (not for the field) in the pojo and as long as your setter name is a match w/ the json prop., there is no problem.  

11. **@PathVariable**
    * This is part of Spring web annot.  
    * This is to map a method param to an incoming request param.  

12. **Model vs ModelMap vs ModelAndView**
    * All these are holders for model attributes and helps in passing them to the views for them to render.  
    * Model:  
        * this is from spring ui package.  
        * This is actually an interface.  
    * ModelMap:  
        * this is nothing but an extension of LinkedHashMap.   
        * That means, this is ordered and maintains an insertion order but hence at the same time it will take more memory compared to an HashMap.  
        * The LinkedHashMap uses a doubly linked-list to keep track of insertions and hence this will take more memory compared to HashMap.  
        * ModelMap is not bound to spring mvc but still does the same task of rendering views.  
    * ModelAndView:
        * is from the spring web servlet package.  
        * This is for holding both Model and the view name, din't find it much useful it except for the fact that you can put the view name in its constructore itself (instead as a return string).  

13. **Autowiring fails with a NoSuchBeanDefinitionException, following could be the reasons:**
    * when the qualifying bean has not been annot. w/ @Component or @Controller or any another stereotype annot.  
    * if you autowired an interface then you must use a @Qualifier to let spring specificially know which implementation of that interface has to be wired.  

14. **@Qualifier**
    * This takes a string and that is actually used to specify the name of the qualifying bean that needs to be autowired.  
    * Used especially when you are autowiring an interface and since an interface can have multiple implementations, it becomes necessary to explicitly mention the name of the qualifying bean/implementation which we want to be auto-wired.  

15. **Stereotype Annot.**
    * @Component, @@Controller, @Indexed, @Repository, @Service - these are the stereotype annot.  
    * These annot. basically are for auto-detection and classpath scanning.  
    * If you autowire a bean then the qualifying bean has to be annot. w/ one of these sterotype annot. for spring to pick them up otherwise a NoSuchBeanDefinitionException will be thrown.  
    * Basically, @Component is the base stereotype annot. and all others mentioned above are special cases of that but more or less anything will do the same.  

16. **@InitBinder**
    * This annot. is used on a method and its purpose is to customize request parameters, template uri variable and backing/command objects.   
    * command/backing objects are nothing but pojos/entities.  
    * This annot. is basically used on a method inside a controller.  
    * Methods annot. with this support all arguments types that handler methods support and WebDataBinder is one of them. Command objects are not supported. **what does this mean?**  
    * The methods annot. w/ this are called in every HTTP request if the 'value' attr is not mentioned. **should explain with example??**  
    * To be more specific about which objects this applies to, mention the value attr. Value takes single/multiple names of command/request attrbs.  
    * There is no limitation to how many methods w/ this annot. can be.  
    * The value attribute should be same as the model attributes key. For e.g.For model.addAttribute("someKey", object); the value of InitBinder annot. should be @InitBinder("someKey"), if you want the method w/ the binder be invoked only for that particular request.  

17. **Flow of @InitBinder and Validator**
    * As soon as you add a model to the modelAttribute, Spring immediately looks for a matching @InitBinder and such a method if present will be called.  
    * And in the @InitBinder method, if the WebDataBinder is configured with a validator by doing webDataBinder.setValidator(new <Validator_Object>) then the validator's support method is called to see compatibility between the passed object in the model against the object that is used to prove true in the supports method of the validator.  

18. **WebDataBinder**
    * This extends DataBinder.  
    * This is used to register custom formatters, validators and propertyeditors.  
    * Basically, this is for binding request params to java bean objects.  
    * Whenever you are using this it is highly recommended to mention the allowedFields otheriwse there is a security risk because in case of an http post form submittion, a malicious client can attempt to send an application by spplying values for fields that do not exist.  

19. **DataBinder setAllowedFields**
    * Register fields that should be allowed for binding.  
    * Default is all fields.  
    * Restrict this, for example to avoid unwanted modifications by malicious users when binding HTTP request parameters.  
    * **HIGHLY IMPORTANT - SECURITY RISK.**    
    * or use setDisallowedFields : which is to register fields that should not be allowed for binding. mark fields as disallowed to avoid unwanted modifications by malicious users when binding http req params.   
    * If you disallow all fields then there will be nothing for data binding and might throw an error:   
        * 2019-03-14 14:02:28.497 DEBUG 17085 --- [nio-8080-exec-3] o.springframework.validation.DataBinder  : Field [lastname] has been removed from PropertyValues and will not be bound, because it has not been found in the list of allowed fields   

