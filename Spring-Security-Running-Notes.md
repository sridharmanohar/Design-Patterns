1. **Spring Boot with Maven**
    * Spring Boot provides a *spring-boot-starter-security* starter which aggregates Spring Security related dependencies together.  

2. **Current Version of Spring Security**
    * 5.1  

3. **Project Modules**
    * **Core** - spring-security-core.jar  
        * this module is required by any application which uses Spring Security  
        * Contains core authentication and access-contol classes and interfaces  
        * the top-level packages in this module are:
            * org.springframework.security.core  
            * org.springframework.security.access  
            * org.springframework.security.authentication  
            * org.springframework.security.provisioning  
            * **which of these packages have I used in the examples code I have seen so far??**  
    * **Web** - spring-security-web.jar  
        * You’ll need it if you require Spring Security web authentication services and URL-based access-control.  
        * Contains filters and related web-security infrastructure code.  
        * Main package:  
            * org.springframework.security.web  
            * ** have I used this package in the REST API examples so far??**  
    * **Config** - spring-security-config.jar  
        * You need it if you are using the Spring Security XML namespace for configuration or Spring Security’s Java Configuration support.  
        * Contains the security namespace parsing code & Java configuration code.  
        * Main package:  
            * org.springframework.security.config  
            * **have I used this package so far in the REST API examples so far??**  
        * None of the classes are intended for direct use in an application.  
    * **OAuth 2.0 Core** - spring-security-oauth2-core.jar  
        * It is required by applications that use OAuth 2.0 or OpenID Connect Core 1.0, such as Client, Resource Server, and Authorization Server.  
        * contains core classes and interfaces that provide support for the OAuth 2.0 Authorization Framework and for OpenID Connect Core 1.0  
        * Main package:  
            * org.springframework.security.oauth2.core  
            * **have I used this package in the REST API examples I have seen so far??**  
    * **OAuth 2.0 Client** - spring-security-oauth2-client.jar  
        * Required by applications leveraging OAuth 2.0 Login and/or OAuth Client support.  
        * Main package:  
            * org.springframework.security.oauth2.client  
    * **OAuth 2.0 JOSE** - spring-security-oauth2-jose.jar  
        * The JOSE framework is intended to provide a method to securely transfer claims between parties.  
        * It is built from a collection of specifications:  
            * JSON Web Token (JWT)   
            * JSON Web Signature (JWS)   
            * JSON Web Encryption (JWE)   
            * JSON Web Key (JWK)   
        * Main packages:  
            * org.springframework.security.oauth2.jwt  
            * org.springframework.security.oauth2.jose  
            * **which of these packages have I used so far??**   
4. **WebSecurityConfigurerAdapter and HttpSecurity** 
    * belongs to org.springframework.security.config top-level package  
    * its an abstract class  
    * its configure(HttpSecurity http) provides a default config. which is as below:  
        *protected void configure(HttpSecurity http) throws Exception {*  
            *http*  
            *.authorizeRequests()*  
                *.anyRequest().authenticated()*  
                *.and()*  
            *.formLogin()*  
                *.and()*  
            *.httpBasic();*  
        *}*  
    * which bascially says:  
        * Ensures that any request to our application requires the user to be authenticated   
        * Allows users to authenticate with form based login   
        * Allows users to authenticate with HTTP Basic authentication   
        * The Java Configuration equivalent of closing an XML tag is expressed using the and() method  
        * **what does authorizeRequests() signify??**  
        * **what is http basic authentication**??  
    * We have to override this method to customize HttpSecurity for our application otherwise the default config will be effective.  
    * by the way, HttpSecurity is a final class in the same top-level package as that of WebSecurityConfigurerAdapter and it allows configuring web based security for http request.  
5. **Java Configuration and Form Login**
    * In case of a webapp, you might be wondering where the login form came from when you were prompted to log in, since we made no mention of any HTML files or JSPs  
    * Since Spring Security’s default configuration does not explicitly set a URL for the login page, Spring Security generates one automatically  
    * While the automatically generated log in page is convenient to get up and running quickly, most applications will want to provide their own log in page. To do so we can update our configuration as seen below:  
    *protected void configure(HttpSecurity http) throws Exception {*  
    *http*  
        *.authorizeRequests()*  
            *.anyRequest().authenticated()*  
            *.and()*  
        *.formLogin()*  
            *.loginPage("/login") 1*  
            *.permitAll();        2*  
    *}*    
    * The updated configuration specifies the location of the log in page.  
    * We must grant all users (i.e. unauthenticated users) access to our log in page. The formLogin().permitAll() method allows granting access to all users for all URLs associated with form based log in.  
6. **Authorize Requests**
    * We can specify custom auth. requirements for our URLs by adding mutiple children to http.authorizeRequests()  
    *protected void configure(HttpSecurity http) throws Exception {*  
    *http*  
        *.authorizeRequests()*  
            *.antMatchers("/resources/**", "/signup", "/about").permitAll()*  
            *.antMatchers("/admin/**").hasRole("ADMIN")*  
            *.antMatchers("/db/**").access("hasRole('ADMIN') and hasRole('DBA')")*  
            *.anyRequest().authenticated()*  
            *.and()*  
        // ...
        *.formLogin();*
      *}*  
    * In the above example, There are multiple children to the http.authorizeRequests() method and each matcher is considered in the order they were declared.  
    * any user can access a request if the URL starts with "/resources/", equals "/signup", or equals "/about".  
    * Any URL that starts with "/admin/" will be restricted to users who have the role "ROLE_ADMIN". You will notice that since we are invoking the hasRole method we do not need to specify the "ROLE_" prefix  
    * Any URL that starts with "/db/" requires the user to have both "ROLE_ADMIN" and "ROLE_DBA". You will notice that since we are using the hasRole expression we do not need to specify the "ROLE_" prefix.  
    * Any URL that has not already been matched on only requires that the user be authenticated  
7. **Handling Logouts**
    * When using the WebSecurityConfigurerAdapter, logout capabilities are automatically applied.  
    * The default is that accessing the URL /logout will log the user out by:  
        * Invalidating the HTTP Session   
        * Cleaning up any RememberMe authentication that was configured **what is RememberMe??**     
        * Clearing the SecurityContextHolder  **what does a SecurityContextHolder contain??**  
        * Redirect to /login?logout  
    * however, you also have various options to further customize your logout requirements:
      *protected void configure(HttpSecurity http) throws Exception {*  
       *http*  
        *.logout()*  
            *.logoutUrl("/my/logout")*  
            *.logoutSuccessUrl("/my/index")*  
            *.logoutSuccessHandler(logoutSuccessHandler)*  
            *.invalidateHttpSession(true)*  
            *.addLogoutHandler(logoutHandler)*  
            *.deleteCookies(cookieNamesToClear)*   
            *.and()*  
        *...*  
       *}*  
    * logoutUrl has The URL that triggers log out to occur (default is /logout). If CSRF protection is enabled (default), then the request must also be a POST.  
    * logoutSuccessUrl has The URL to redirect to after logout has occurred. The default is /login?logout  
    * If a custom LogoutSuccessHandler is provided as in the above example then the logoutSuccessUrl() is ignored.  
    * Generally, in order to customize logout functionality, you can add LogoutHandler and/or LogoutSuccessHandler implementations. For many common scenarios, these handlers are applied under the covers when using the fluent API.  
8. **Major building blocks of Spring Security**:
    * SecurityContextHolder  
        * to provide access to SecurityContext  
        * **package? class or interface??**  
    * SecurityContext  
        * to hold the Authentication and possibly request-specific security information  
        * **package? class or interface??**  
    * Authentication  
        * to represent the principal in a Spring Security-specific manner.  
        * **what is a principal??**  
        * **package? class or interface??**  
    * GrantedAuthority  
        * to reflect the application-wide permissions granted to a principal.  
        * **package? class or interface??**  
        * **what does this exactly contain? ROLES??**  
    * UserDetails  
        * to provide the necessary information to build an Authentication object from your application’s DAOs or other source of security data.  
        * **package? class or interface??**  
    * UserDetailsService  
        * to create a UserDetails when passed in a String-based username (or certificate ID or the like).   
        * this is part of top-level package: org.springframework.security.core  
        * this is an interface  
        * it has a single method:  
            * *UserDetails loadUserByUsername(String username) throws UsernameNotFoundException;*    
            * The returned UserDetails is an interface that provides getters that guarantee non-null provision of authentication information such as the username, password, granted authorities and whether the user account is enabled or disabled.  
        * This can be implemented in 2 ways:  
            * In-memory authentication: 
                * where a persistent data store is not needed and a memory map is supplied  
                * but this approach is basically for testing purposes only    
            * JdbcDaoImpl: 
                * this implementation of UserDetailsService can obtain authentication information from a JDBC data source  
                * Internally Spring JDBC is used  
                * This is a class  
                * this implementation assumes a default schema consisting of 2 tables - users and authorities  
                * *users table*: username, password and enabled  
                * *authorities table*: username, authority  
    * **how does spring security fit in applications like the REST API examples that I have seen which has OAuth also?? I know Spring Security does the authentication and OAuth does the authorization but what exactly does spring security authenticate in such application and when is it called, before OAuth or after??**  
9. **What is authentication in Spring Security?**
    * Lets consider a standard authentication scenario that everyone is familiar with.  
        * A user is prompted to log in with a username and password.  
        * The system (successfully) verifies that the password is correct for the username.   
        * The context information for that user is obtained (their list of roles and so on).   
        * A security context is established for the user   
        * The user proceeds, potentially to perform some operation which is potentially protected by an access control mechanism which checks the required permissions for the operation against the current security context information.   
    * The first three items constitute the authentication process so we’ll take a look at how these take place within Spring Security.  
        * The username and password are obtained and combined into an instance of *UsernamePasswordAuthenticationToken* (an instance of the Authentication interface)  
        * The token is passed to an instance of AuthenticationManager for validation. **you mean an instance of UsernamePasswordAuthenticationToken is passed??**  
        * The AuthenticationManager returns a fully populated Authentication instance on successful authentication.   
        * The security context is established by calling SecurityContextHolder.getContext().setAuthentication(…​), passing in the returned authentication object.   
        * Basically, A user is authenticated when the SecurityContextHolder contains a fully populated Authentication object.  
        * **in which package are UsernamePasswordAuthenticationToken, AuthenticationManager, Authentication, SecurityContextHolder are present??**  
10. **Authentication Mechanism**
    * This is true mainly in case of web application authentication  
    * Once your browser submits your authentication credentials (either as an HTTP form post or HTTP header) there needs to be something on the server that "collects" these authentication details.  
    * In Spring Security we have a special name for the function of collecting authentication details from a user agent (usually a web browser), referring to it as the "authentication mechanism"  
    * Examples are form-base login and Basic authentication  
    * Once the authentication details have been collected from the user agent, an Authentication "request" object is built and then presented to the AuthenticationManager.  
    * After the authentication mechanism receives back the fully-populated Authentication object, it will deem the request valid, put the Authentication into the SecurityContextHolder. If, on the other hand, the AuthenticationManager rejected the request, the authentication mechanism will ask the user agent to retry.  
11. **CSRF**
    * Cross-site request forgery, also known as one-click attack or session riding or XSRF, is a type of malicious exploit of a website where unauthorized commands are transmitted from a user that the web application trusts.  
    * Unlike cross-site scripting (XSS), which exploits the trust a user has for a particular site, CSRF exploits the trust that a site has in a user's browser.   
    * Our recommendation is to use CSRF protection for any request that could be processed by a browser by normal users. If you are only creating a service that is used by non-browser clients, you will likely want to disable CSRF protection.  
    * What if my application is stateless? That doesn’t necessarily mean you are protected. In fact, if a user does not need to perform any actions in the web browser for a given request, they are likely still vulnerable to CSRF attacks.  
    * Users using basic authentication are also vulnerable to CSRF attacks since the browser will automatically include the username password in any requests  
    * The steps to using Spring Security’s CSRF protection are outlined below:  
        * Use proper HTTP verbs:  
            * The first step to protecting against CSRF attacks is to ensure your website uses proper HTTP verbs.  
            * you need to be certain that your application is using PATCH, POST, PUT, and/or DELETE for anything that modifies state.  
            * This is not a limitation of Spring Security’s support, but instead a general requirement for proper CSRF prevention. The reason is that including private information in an HTTP GET can cause the information to be leaked.  
        * Configure CSRF Protection  
            * The next step is to include Spring Security’s CSRF protection within your application **which is by default enabled since Spring Security 4.0**    
            * If you want to disable this, following is how you do it with java config.  
                * in the class which extends WebSecurityConfigurerAdapter, override the configure(HttpSecurity http) method and disable csrf in this.  
        * Including CSRF token in form submissions and ajax and json requests  
            * not going into the details of this approach  
            * it is a not a simple approach, has its own disadvantages, so should know well before implementing  
            * read CSRF Caveats before implementing  
12. **CORS**
    * Cross-Origin Resource Sharing (CORS) is a mechanism that uses additional HTTP headers to tell a browser to let a web application running at one origin (domain) have permission to access selected resources from a server at a different origin.  
    * For security reasons, browsers prohibit AJAX calls to resources outside the current origin. For example, you could have your bank account in one tab and evil.com in another. Scripts from evil.com should not be able to make AJAX requests to your bank API with your credentials — for example withdrawing money from your account!  
    * Cross-Origin Resource Sharing (CORS) is a W3C specification implemented by most browsers that lets you specify what kind of cross-domain requests are authorized  
    * Spring MVC lets you handle CORS  
    * The easiest way to ensure that CORS is handled first is to use the CorsFilter. Users can integrate the CorsFilter with Spring Security by providing a CorsConfigurationSource using the following:  
        *@EnableWebSecurity*  
        *public class WebSecurityConfig extends WebSecurityConfigurerAdapter {*  
        *@Override*  
        *protected void configure(HttpSecurity http) throws Exception {*  
            *http*  
                *.cors().and()*  
                *some code here*  
        *}*  
        *@Bean*  
        *CorsConfigurationSource corsConfigurationSource() {*  
            *CorsConfiguration configuration = new CorsConfiguration();*  
            *configuration.setAllowedOrigins(Arrays.asList("https://example.com"));*  
            *configuration.setAllowedMethods(Arrays.asList("GET","POST"));*  
            *UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();*  
            *source.registerCorsConfiguration("/twoasterikshere-removed coz of markdown issues", configuration);*  
            *return source;*  
        }}  
    * When you invoke cors method of HttpSecurity, If a bean by the name of corsFilter is provided, that CorsFilter is used. Else if corsConfigurationSource is defined, then that CorsConfiguration is used.  
    * CorsConfigurationSource:  
        * its an interface in org.springframework.web.cors package  
    * UrlBasedCorsConfigurationSource:  
        * its an implementation of CorsConfigurationSource interface  
        * its in the org.springframework.web.cors package  
        * it allows you to register a CorsConfiguration using its registerCorsConfiguration method (which takes a CorsConfiguration instance)  
    * CorsConfiguration:  
        * its a class and
        * its in the package org.springframework.web.cors  
        * this is where you set the cors configurations  
        * By default a newly created CorsConfiguration does not permit any cross-origin requests and must be configured explicitly to indicate what should be allowed.  
        * Use applyPermitDefaultValues() to flip the initialization model to start with open defaults that permit all cross-origin requests for GET, HEAD, and POST requests.  
    * If you are using Spring MVC’s CORS support, you can omit specifying the CorsConfigurationSource and Spring Security will leverage the CORS configuration provided to Spring MVC i.e. a HandlerMappingIntrospector is used.  
13. **EnableGlobalMethodSecurity**
    * We can enable annotation-based security using the @EnableGlobalMethodSecurity annotation on any @Configuration instance  
    * This is a class-level annot.  
    * This annot has following optional elements/attributes:  
        *  @EnableGlobalMethodSecurity(securedEnabled = true)  
            * Determines if Spring Security's Secured annotations should be enabled. Default is false.
            * The @Secured annotation is used to specify a list of roles on a method. Hence, a user only can access that method if she has at least one of the specified roles.  
                *@Secured("ROLE_VIEWER")*  
                *public String getUsername() {*  
                    *SecurityContext securityContext = SecurityContextHolder.getContext();*  
                    *return securityContext.getAuthentication().getName();*  
                *}*  
            * Here, the @Secured(“ROLE_VIEWER”) annotation defines that only users who have the role ROLE_VIEWER are able to execute the getUsername method.  
            * we can also define a list of roles in a @Secured annotation
            * The @Secured annotation doesn’t support Spring Expression Language (SpEL).
        * @EnableGlobalMethodSecurity(jsr250Enabled = true)  
            * this will enable support for jsr-250 annotations  
            * The @RoleAllowed annotation is the JSR-250’s equivalent annotation of the @Secured annotation.  
            * Basically, we can use the @RoleAllowed annotation in a similar way as @Secured:  
                *@RolesAllowed("ROLE_VIEWER")*  
                *public String getUsername2() {*  
                  *//...*   
                 *}*  
            * Similarly, only the user who has role ROLE_VIEWER can execute getUsername2.  
        * @EnableGlobalMethodSecurity(prePostEnabled = true)  
            * this enables support for Spring Security's pre post annotations.  
            * these annot. can be written in SpEL  
            * @PreAuthorize  
                * checks the given expression before entering the method  
                    *@PreAuthorize("hasRole('ROLE_VIEWER')")*  
                    *public String getUsernameInUpperCase() {*  
                    *return getUsername().toUpperCase();*  
                    *}*  
                * The @PreAuthorize(“hasRole(‘ROLE_VIEWER’)”) has the same meaning as @Secured(“ROLE_VIEWER”) which we used in the previous section  
                * Moreover, we can actually use the method argument as part of the expression:  
                    *@PreAuthorize("#username == authentication.principal.username")*  
                        *public String getMyRoles(String username) {*  
                            *some code here*  
                     *}*  
                    * Here, a user can invoke the getMyRoles method only if the value of the argument username is the same as current principal’s username.  
            * @PostAuthorize  
                * checks the given expression after the execution of the method and could alter the result  
                * an example:  
                    *@PostAuthorize("#username == authentication.principal.username")*  
                    *public String getMyRoles2(String username) {*  
                        *some code here*  
                    *}*  
                    * here, the authorization would get delayed after the execution of the target method.      
                * Additionally, the @PostAuthorize annotation provides the ability to access the method result:  
                    *@PostAuthorize("returnObject.username == authentication.principal.nickName")*  
                    *public CustomUser loadUserDetail(String username) {*  
                        *return userRoleRepository.loadUserByUserName(username);*  
                        *}*  
                    * In this example, the loadUserDetail method would only execute successfully if the username of the returned CustomUser is equal to the current authentication principal’s nickname.  
            * @PreFilter  
                * Spring Security provides the @PreFilter annotation to filter a collection argument before executing the method  
                    *@PreFilter("filterObject != authentication.principal.username")*  
                        *public String joinUsernames(List<String> usernames) {*  
                            *return usernames.stream().collect(Collectors.joining(";"));*  
                        *}*  
                    * In this example, we’re joining all usernames except for the one who is authenticated.  
                    * Here, our expression uses the name filterObject to represent the current object in the collection. However, if the method has more than one argument which is a collection type, we need to use the filterTarget property to specify which argument we want to filter  
            * @PostFilter  
                * we can filter the returned collection of a method by using this annot.  
                    *@PostFilter("filterObject != authentication.principal.username")*  
                        *public List<String> getAllUsernamesExceptCurrent() {*  
                            *return userRoleRepository.getAllUsernames();*  
                        *}*  
                * In this case, the name filterObject refers to the current object in the returned collection.  
                * With that configuration, Spring Security will iterate through the returned list and remove any value which matches with the principal’s username.  
    * Method Security Meta-Annotation  
        * We typically find ourselves in a situation where we protect different methods using the same security configuration. In this case, we can define a security meta-annotation:  
            *@Target(ElementType.METHOD)*  
            *@Retention(RetentionPolicy.RUNTIME)*  
            *@PreAuthorize("hasRole('VIEWER')")*  
            *public @interface IsViewer {*  
            *}*      
        * Next, we can directly use the @IsViewer annotation to secure our method: 
            *@IsViewer*  
            *public String getUsername4() {*  
                *some code here*  
            *}*  
        * Security meta-annotations are a great idea because they add more semantics and decouple our business logic from the security framework.  
    * Security Annotation at the Class Level  
        * If we find ourselves using the same security annotation for every method within one class, we can consider putting that annotation at class level:  
            *@Service*  
            *@PreAuthorize("hasRole('ROLE_ADMIN')")*  
            *public class SystemService {*  
                *public String getSystemYear(){*  
                    *some code here*  
                *}*  
            *public String getSystemDate(){*  
                *some code here*  
            *}*  
            *}*  
        * In above example, the security rule hasRole(‘ROLE_ADMIN’) will be applied to both getSystemYear and getSystemDate methods.  
    * Multiple Security Annotations on a Method  
        * We can also use multiple security annotations on one method:  
            *@PreAuthorize("#username == authentication.principal.username")*  
            *@PostAuthorize("returnObject.username == authentication.principal.nickName")*  
            *public CustomUser securedLoadUserDetail(String username) {*  
                *return userRoleRepository.loadUserByUserName(username);*  
            *}*  
        * Hence, Spring will verify authorization both before and after the execution of the securedLoadUserDetail method.  
    * If you want to use more complicated security opertaions that are possible with @EnableGloablMethodSecurity then you can extend GlobalMethodSecurityConfiguration. You still have to have @EnableGloablMethodSecurity(prePostEnabled = true) on this subclass.  
    * The method security in spring is based on aop.  
14. **Why not just use web.xml security?**
    * Let’s assume you’re developing an enterprise application based on Spring. There are four security concerns you typically need to address:  
        * authentication  
            * The servlet specification provides an approach to authentication. However, you will need to configure the container to perform authentication which typically requires editing of container-specific "realm" settings. This makes a non-portable configuration, and if you need to write an actual Java class to implement the container’s authentication interface, it becomes even more non-portable.  
            * With Spring Security you achieve complete portability  
            * Also, Spring Security offers a choice of production-proven authentication providers and mechanisms, meaning you can switch your authentication approaches at deployment time. This is particularly valuable for software vendors writing products that need to work in an unknown target environment.   
        * web request security  
            * The servlet specification provides an approach to secure your request URIs. However, these URIs can only be expressed in the servlet specification’s own limited URI path format.  
            * Spring Security provides a far more comprehensive approach. For instance, you can use Ant paths or regular expressions, you can consider parts of the URI other than simply the requested page (e.g. you can consider HTTP GET parameters) and you can implement your own runtime source of configuration data.  
        * service layer security (i.e. your methods that implement business logic)  
            * The absence of support in the servlet specification for services layer security or domain object instance security represent serious limitations for multi-tiered applications.  
            * Typically developers either ignore these requirements, or implement security logic within their MVC controller code (or even worse, inside the views).  
            * There are serious disadvantages with this approach:  
                * Separation of concerns:  
                    * Authorization is a crosscutting concern and should be implemented as such.  
                    * MVC controllers or views implementing authorization code makes it more difficult to test both the controller and authorization logic, more difficult to debug, and will often lead to code duplication.   
                * Layering issues:   
                    * An MVC controller or view is simply the incorrect architectural layer to implement authorization decisions concerning services layer methods or domain object instances.  
                    * Whilst the Principal may be passed to the services layer to enable it to make the authorization decision, doing so would introduce an additional argument on every services layer method.  
                    * A more elegant approach is to use a ThreadLocal to hold the Principal, although this would likely increase development time to a point where it would become more economical (on a cost-benefit basis) to simply use a dedicated security framework.   
                * Authorisation code quality:  
                    * Writing your own authorization code from scratch does not provide the "design check" a framework would offer, and in-house authorization code will typically lack the improvements that emerge from widespread deployment, peer review and new versions.
    * For simple applications, servlet specification security may just be enough. Although when considered within the context of web container portability, configuration requirements, limited web request security flexibility, and non-existent services layer and domain object instance security, it becomes clear why developers often look to alternative solutions.
15. **When I try to log in, I get an error message that says "Bad Credentials". What’s wrong?  **
    * This means that authentication has failed. It doesn’t say why, as it is good practice to avoid giving details which might help an attacker guess account names or passwords.  
    * This also means that if you ask this question in the forum, you will not get an answer unless you provide additional information.  
    * As with any issue you should check the output from the debug log, note any exception stacktraces and related messages. Step through the code in a debugger to see where the authentication fails and why. Write a test case which exercises your authentication configuration outside of the application.  
    * More often than not, the failure is due to a difference in the password data stored in a database and that entered by the user.  
    * If you are using hashed passwords, make sure the value stored in your database is exactly the same as the value produced by the PasswordEncoder configured in your application.  
16. **My application goes into an "endless loop" when I try to login, what’s going on?**
    * A common user problem with infinite loop and redirecting to the login page is caused by accidently configuring the login page as a "secured" resource.  
    * Make sure your configuration allows anonymous access to the login page, either by excluding it from the security filter chain or marking it as requiring ROLE_ANONYMOUS.  
17. **Why can I still see a secured page even after I’ve logged out of my application?**
    * The most common reason for this is that your browser has cached the page and you are seeing a copy which is being retrieved from the browsers cache.  
    * Verify this by checking whether the browser is actually sending the request (check your server access logs, the debug log or use a suitable browser debugging plugin such as "Tamper Data" for Firefox).  
    * This has nothing to do with Spring Security and you should configure your application or server to set the appropriate Cache-Control response headers.  
    * Note that SSL requests are never cached.  
18. **I’m using Spring Security’s concurrent session control to prevent users from logging in more than once at a time.**  
    * When I open another browser window after logging in, it doesn’t stop me from logging in again. Why can I log in more than once?  
    * The server doesn’t know anything about tabs, windows or browser instances. All it sees are HTTP requests and it ties those to a particular session according to the value of the JSESSIONID cookie that they contain.  
    * When a user authenticates during a session, Spring Security’s concurrent session control checks the number ofother authenticated sessions that they have.  
    * If they are already authenticated with the same session, then re-authenticating will have no effect.  
19. **Why does the session Id change when I authenticate through Spring Security?**
    * With the default configuration, Spring Security changes the session ID when the user authenticates.  
    * If you’re using a Servlet 3.1 or newer container, the session ID is simply changed.  
    * If you’re using an older container, Spring Security invalidates the existing session, creates a new session, and transfers the session data to the new session. Changing the session identifier in this manner prevents"session-fixation" attacks.  
20. **I’m using Tomcat (or some other servlet container) and have enabled HTTPS for my login page, switching back to HTTP afterwards. It doesn’t work - I just end up back at the login page after authenticating.**
    * This happens because sessions created under HTTPS, for which the session cookie is marked as "secure", cannot subsequently be used under HTTP.  
    * The browser will not send the cookie back to the server and any session state will be lost (including the security context information).  
    * switching between HTTP and HTTPS is not a good idea in general, as any application which uses HTTP at all is vulnerable to man-in-the-middle attacks.  
    * To be truly secure, the user should begin accessing your site in HTTPS and continue using it until they log out.  
    * Even clicking on an HTTPS link from a page accessed over HTTP is potentially risky.   
21. **I get a 403 Forbidden when performing a POST**
    * If an HTTP 403 Forbidden is returned for HTTP POST, but works for HTTP GET then the issue is most likely related to CSRF.  
    * Either provide the CSRF Token or disable CSRF protection (not recommended).   
22. **What does "ROLE_" mean and why do I need it on my role names?**
    * Spring Security has a voter-based architecture which means that an access decision is made by a series of AccessDecisionVoter s.  
    * The voters act on the "configuration attributes" which are specified for a secured resource  
    * With this approach, not all attributes may be relevant to all voters and a voter needs to know when it should ignore an attribute (abstain) and when it should vote to grant or deny access based on the attribute value.  
    * The most common voter is the RoleVoter which by default votes whenever it finds an attribute with the "ROLE_" prefix. It makes a simple comparison of the attribute (such as "ROLE_USER") with the names of the authorities which the current user has been assigned.  
    * If it finds a match (they have an authority called "ROLE_USER"), it votes to grant access, otherwise it votes to deny access.  
22. **How do I know which dependencies to add to my application to work with Spring Security?**
    * All applications will need the spring-security-core jar.  
    * If you’re developing a web application, you need the spring-security-web jar.  
    * If you’re using security namespace configuration you need the spring-security-config jar  
    * If you are building your project with maven, then adding the appropriate Spring Security modules as dependencies to your pom.xml will automatically pull in the core jars that the framework requires.  
    * any which are marked as "optional" in the Spring Security POM files will have to be added to your own pom.xml file if you need them.  
23. **What is a UserDetailsService and do I need one?**
    * UserDetailsService is a DAO interface for loading data that is specific to a user account.  
    * It has no other function other to load that data for use by other components within the framework.  
    * It is not responsible for authenticating the user.  
    * Authenticating a user with a username/password combination is most commonly performed by the DaoAuthenticationProvider, which is injected with a UserDetailsService to allow it to load the password (and other data) for a user in order to compare it with the submitted value.  
    * If you want to customize the authentication process then you should implement AuthenticationProvider yourself.  
24. **I need to login in with more information than just the username.**
    * The submitted login information is processed by an instance of UsernamePasswordAuthenticationFilter. You will need to customize this class to handle the extra data field(s).  
    * One option is to use your own customized authentication token class (rather than the standard UsernamePasswordAuthenticationToken)  
        * If you are using a custom authentication token class, for example, you will have to write an AuthenticationProvider to handle it (or extend the standard DaoAuthenticationProvider).   
    * another is simply to concatenate the extra fields with the username (for example, using a ":" as the separator) and pass them in the username property of UsernamePasswordAuthenticationToken.  
        * If you have concatenated the fields, you can implement your own UserDetailsService which splits them up and loads the appropriate user data for authentication.  
25. **How do I apply different intercept-url constraints where only the fragment value of the requested URLs differs (e.g./foo#bar and /foo#blah?**
    * You can’t do this, since the fragment is not transmitted from the browser to the server. The URLs above are identical from the server’s perspective.  
26. **How do I access the user’s password in a UserDetailsService?**
    * You can’t (and shouldn’t). You are probably misunderstanding its purpose.  
27. **Authorization Server (OAuth2 and SpringBoot)**
    * Minimal OAuth2 Boot Configuration  
        * Creating a minimal Spring Boot authorization server consists of three basic steps:  
            * Including the dependencies.   
                * To use the auto-configuration features in this library, you need spring-security-oauth2  
                * and spring-security-oauth2-autoconfigure  
                * **what is the purpose of autoconfigure? why havent this been used in the examples I have seen so far??**  
                * Note that you need to specify the version for spring-security-oauth2-autoconfigure, since it is not managed by Spring Boot any longer, though it should match Boot’s version anyway.  
                * For JWT support, you also need spring-security-jwt              
            * Including the @EnableAuthorizationServer annotation.   
                * Similar to other Spring Boot @Enable annotations, you can add the @EnableAuthorizationServer annotation to the class that contains your main method  
                * Adding this annotation imports other Spring configuration files that add a number of reasonable defaults, such as how tokens ought to be signed, their duration, and what grants to allow.  
            * Specifying at least one client ID and secret pair.   
                * **when are these details used for??**  
                * **are these same as identifier in oauth2 which is used as username and pwd?**  
                * **is this common for all clients??**  
                * **what is the diff b/w these and the ones in spring security java config ??**  
28. **How to Switch Off OAuth2 Boot’s Auto Configuration**
    * Basically, the OAuth2 Boot project creates an instance of AuthorizationServerConfigurer with some reasonable defaults:  
        * It registers a NoOpPasswordEncoder (overriding the Spring Security default)   
        * It lets the client you provided use any grant type this server supports: authorization_code, password, client_credentials, implicit, or refresh_token  
    * if you need to configure more than one client, change their allowed grant types, or use something better than the no-op password encoder (highly recommended!), then you want to expose your own AuthorizationServerConfigurer, as the following example shows:  
        *@Configuration*  
        *public class AuthorizationServerConfig extends AuthorizationServerConfigurerAdapter {*  
   
        *@Autowired DataSource dataSource;*  
  
        *protected void configure(ClientDetailsServiceConfigurer clients) {*  
            *clients*   
                *.jdbc(this.dataSource)*  
                *.passwordEncoder(PasswordEncoderFactories.createDelegatingPasswordEncoder());*  
            *}*  
        *}*  
        * The preceding configuration causes OAuth2 Boot to no longer retrieve the client from environment properties and now falls back to the Spring Security password encoder default.  
        * **what pwds are we encoding here??**  
        * **what type of grants have I seen in the examples I have seen so far in spring security + Oauth??**  
29. **Resource Server (Oauth2 and SpringBoot)**
    * Spring Security OAuth2 Boot simplifies protecting your resources using Bearer Token authentication in two different token formats: JWT and Opaque.  
    * Minimal OAuth2 Boot Configuration  
        * Including the dependencies.   
            * To use the auto-configuration features in this library, you need spring-security-oauth2  
            * and spring-security-oauth2-autoconfigure  
            * Note that you need to specify the version for spring-security-oauth2-autoconfigure, since it is not managed by Spring Boot any longer  
            * For JWT support, you also need spring-security-jwt.  
        * Including the @EnableResourceServer annotation.   
            * Similar to other Spring Boot @Enable annotations, you can add the @EnableResourceServer annotation to the class that contains your main method  
            * Adding this annotation adds the OAuth2AuthenticationProcessingFilter  
        * Specifying a strategy for verifying the bearer token.  
            * Bearer Tokens typically come in one of two forms: JWT-encoded or opaque. You will need to configure the resource server with one or the other strategy.  
                                                    