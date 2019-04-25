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

## @PathVariable
1. This is part of Spring web annot.
2. This is to map a method param to an incoming request param.

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
8. The value attribute should be same as the model attributes key. For e.g.For model.addAttribute("someKey", object); the value of InitBinder annot. should be @InitBinder("someKey"), if you want the method w/ the binder be invoked only for that particular request.

## Flow of @InitBinder and Validator
1. As soon as you add a model to the modelAttribute, Spring immediately looks for a matching @InitBinder and such a method if present will be called.
2. And in the @InitBinder method, if the WebDataBinder is configured with a validator by doing webDataBinder.setValidator(new <Validator_Object>) then the validator's support method is called to see compatibility between the passed object in the model against the object that is used to prove true in the supports method of the validator.

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
