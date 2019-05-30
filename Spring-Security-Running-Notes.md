1. **Spring Boot with Maven**
    * Spring Boot provides a spring-boot-starter-security starter which aggregates Spring Security related dependencies together.  
2. **Current Version of Spring Security**
    * 5.1  
3. **Project Modules**
    * Core - spring-security-core.jar  
        * this module is required by any application which uses Spring Security  
        * Contains core authentication and access-contol classes and interfaces  
        * the top-level packages in this module are:
            * org.springframework.security.core  
            * org.springframework.security.access  
            * org.springframework.security.authentication  
            * org.springframework.security.provisioning  
    * Web - spring-security-web.jar  
        * You’ll need it if you require Spring Security web authentication services and URL-based access-control.  
        * Contains filters and related web-security infrastructure code.  
        * Main package:  
            * org.springframework.security.web  
    * Config - spring-security-config.jar  
        * You need it if you are using the Spring Security XML namespace for configuration or Spring Security’s Java Configuration support.  
        * Contains the security namespace parsing code & Java configuration code.  
        * Main package:  
            * org.springframework.security.config  
        * None of the classes are intended for direct use in an application.  
    * OAuth 2.0 Core - spring-security-oauth2-core.jar  
        * It is required by applications that use OAuth 2.0 or OpenID Connect Core 1.0, such as Client, Resource Server, and Authorization Server.  
        * contains core classes and interfaces that provide support for the OAuth 2.0 Authorization Framework and for OpenID Connect Core 1.0  
        * Main package:  
            * org.springframework.security.oauth2.core  
    * OAuth 2.0 Client - spring-security-oauth2-client.jar  
        * Required by applications leveraging OAuth 2.0 Login and/or OAuth Client support.  
        * Main package:  
            * org.springframework.security.oauth2.client  
    * OAuth 2.0 JOSE - spring-security-oauth2-jose.jar  
        * The JOSE framework is intended to provide a method to securely transfer claims between parties.  
        * It is built from a collection of specifications:  
            * JSON Web Token (JWT)   
            * JSON Web Signature (JWS)   
            * JSON Web Encryption (JWE)   
            * JSON Web Key (JWK)   
        * Main packages:  
            * org.springframework.security.oauth2.jwt  
            * org.springframework.security.oauth2.jose  
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
    * We have to override this method to HttpSecurity for our application otherwise the default config will be effective.  
    * by the way, HttpSecurity is a final class in the same top-level package as that of WebSecurityConfigurerAdapter and it allows configuring web based security for http request.  
5. **Java Configuration and Form Login**
    * You might be wondering where the login form came from when you were prompted to log in, since we made no mention of any HTML files or JSPs  
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
        * Cleaning up any RememberMe authentication that was configured   
        * Clearing the SecurityContextHolder  
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
    * SecurityContext  
        * to hold the Authentication and possibly request-specific security information  
    * Authentication  
        * to represent the principal in a Spring Security-specific manner.  
    * GrantedAuthority  
        * to reflect the application-wide permissions granted to a principal.  
    * UserDetails  
        * to provide the necessary information to build an Authentication object from your application’s DAOs or other source of security data.  
    * UserDetailsService  
        * to create a UserDetails when passed in a String-based username (or certificate ID or the like).   
        * this is part of top-level package: org.springframework.security.core  
        * this is an interface  
        * it has a single method:  
            * UserDetails loadUserByUsername(String username) throws UsernameNotFoundException;  
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
                * users table: username, password and enabled  
                * authorities table: username, authority  
9. **What is authentication in Spring Security?**
   * Let’s consider a standard authentication scenario that everyone is familiar with.  
        * A user is prompted to log in with a username and password.  
        * The system (successfully) verifies that the password is correct for the username.   
        * The context information for that user is obtained (their list of roles and so on).   
        * A security context is established for the user   
        * The user proceeds, potentially to perform some operation which is potentially protected by an access control mechanism which checks the required permissions for the operation against the current security context information.   
    * The first three items constitute the authentication process so we’ll take a look at how these take place within Spring Security.  
        * The username and password are obtained and combined into an instance of UsernamePasswordAuthenticationToken (an instance of the Authentication interface)  
        * The token is passed to an instance of AuthenticationManager for validation.   
        * The AuthenticationManager returns a fully populated Authentication instance on successful authentication.   
        * The security context is established by calling SecurityContextHolder.getContext().setAuthentication(…​), passing in the returned authentication object.   
        * Basically, A user is authenticated when the SecurityContextHolder contains a fully populated Authentication object.  
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
            * The next step is to include Spring Security’s CSRF protection within your application which is by default enabled since Spring Security 4.0  
            * If you want to disable this, following is how you do it with java config.  
                * in the class which extends WebSecurityConfigurerAdapter, override the configure(HttpSecurity http) method and disable csrf in this.  
        * Including CSRF token in form submissions and ajax and json requests  
            * not going into the details of this approach  
            * it is a not a simple approach, has its own disadvantages, so should know well before implementing  
            * read CSRF Caveats before implementing  
   

                                                   