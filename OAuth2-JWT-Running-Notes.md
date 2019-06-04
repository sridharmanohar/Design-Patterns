1. **OAuth2**
    * OAuth or OAuth2 stands for Open Authorization.  
    * Its a free and Open protocol.  
    * It allows users to share their private resources with a third-party while keeping their credentials secret. These resources could be photos, videos etc.  
    * OAuth does this by granting the requesting (client) a token, once access is approved by the user. Each token grants limited access to a specific resource for a specific period.  
    * The OAuth 1.0 was a result of a small community based effort, built to support certain use-cases. OAuth 2.0, is a standard and it is built with the experiences of OAuth 1.0 and other use-cases. 2 is backward compatible with 1.  
   
2. **Accessing restricted resources in traditional client-server model i.e. w/o oauth2**
    * The clients requests access to a protected resource on the server by authenticating with the server using the resource owner's creds. For this to happen, the resource owner must share it's creds with the third-party appi i.e. the client.  
    * There are several limitations of this approach:  
        * The third-party apps must store the user creds with them which can raise security, trust issues.  
        * Whenever the user changes the creds for the protected resource, the same change should also happen at the third-party app - duplication of efforts.  
        * Third-party apps will gain overly broad access to the protected resource and might lead to exploitation.  
  
3. **OAuth2 Roles**
    * There are 4 roles in OAuth2.  
        * Resource Owner:  
            *  an entity capable of granting access to protected resources which it owns. 
            *  When a resource owner is a person, it is referred to as end-user.  
        * Resource Server:  
            * the server hosting the protected resources 
            * and capable of accepting and responding to protected resource requests using access tokens.    
        * Client:  
            * an application making protected resurce requests on behalf of the resource owner and with its authorization.  
        * Authorization Server:  
            * the server issuing access tokens to client after sucessfully authenticating the resource owner and obtaining authorization.  

4. **OAuth2 Protocol Flow**
    * Following is the protocol flow:  
        * the client request authorization from resource owner. The authorization request can be made directly to the resource owner, or preferably indirectly via the authorization server.  
        * the client receives the authorization grant, which is a credential represential resource owner's authorization, expressed using one of four grant types or using an extension grant type. The grant type dependens upon the methd used by the client to request authorization and the types supported by the auth. server.  
        * the client requests an access token by authenticating with the auth server and presenting the auth grant.  
        * the auth server authenticates the client and validates the auth grant, if valid, issues an access token.  
        * the client requests the protected resource from the resource server and authenticates by presenting the access token.  
        * the resource server validates the access token, if valid, serves the request.  

5. **OAuth2 Authorization grant types**
    * Following are the grant types:  
        * Auth. Code:  
            * Here the auth. code is obtained by using an auth. server as an intermediary b/w the client and the resource owner.  
            * Instead of requesting auth. directly from the resource owner, the client directs the resource owner to an auth. server which in turn directs the resource owner back to the client w/ the auth. code but before directing the resource owner back to the client with auth. code, the auth. server authenticates the resource owner and obtains auth.  
            * this is generally used with server-side applications.   
        * Implicit: 
            * this is a simplified auth. code flow optimized for clients implemented in a browser using a scripting language like javascript.  
            * here instead of issuing the auth. code, the client is issued an access token directly.  
            * this is generally used with mobile apps or web apps - apps that run on the user's device.  
        * Resource Owner password Creds (also known as Password grant type):  
            * the resource owner pwd creds (i.e. username and pwd) can be used directly as an auth. grant to obtain an access token.  
            * this should only be used when there is a high degree of trust b/w the resource owner and tthe client.  
            * but even though the resource owner creds are with client, they are with the client for a single reqest and are then exchanged for an access token.  
            * this grant eliminates the need for the client to store the creds for future use, by exchanging creds with a long-lived access token. 
            * this is used with trusted applications, such as those owned by the service itself.  
        * Client creds:  
            * here the client creds are used as auth. grant typically when the client is acting on its own behalf i.e. the client is also the resource owner.  
            * used for machine-to-machine interaction.  
            * used with Applications API access.  

6. **OAuth2 Access Token**
    * Access tokens are strings representing an auth. issued by the auth. server in exchange of the auth. grant to the client to enable the client to access protected resources.  
    * These tokens repesent specific scopes and duration of access.  
    * Access tokens can have different formats, strucrures and cryptographic properties depending upon the resource server security requirements.  
 
7. **OAuth2 Refresh Token**
    * Refresh tokens are creds issued to the clients by the auth. server which are used to obtain fresh/new access tokens when the existing ones become invalid/expire.  
    * These tokens are optional and it depends upon the auth. server whether to issue to refresh tokens or not. But if they are issued, they are issued along with the access tokens itself by the auth. server.  
    * But, unlike access tokens, refresh tokens are intended for use only with the auth. server and are never sent to the resource server.  
    * The flow for getting an refresh token and it's use is as follows:  
        * the client requests an access token by authenticating with the auth. server and presenting an auth. grant.  
        * the auth. server authenticates the client and validates the auth. grant, and if valid, issues an access token and a refresh token.  
        * the client makes a protected resource request to the resource server by presenting an access token.  
        * the resource server validates the access token, and if valid, serves the request.  
        * If the access token is invalid or expired, the resource server returns an invalid token error.  
        * the client requests a new access token by authenticating with the auth. server and presenting the refresh token.  
        * the auth. server authenticates the client and validates the refresh token, and if valid, issues a new access token (and, optionally, a new refresh token).  

8. **OAuth2 Client registration**
    * Before the client initiates the protocol, it has to register with the auth. server.  
    * This reg. can happen in many ways but typically involves an end-user interaction with an html form and filling out a few details.  

9. **OAuth2 Client Types**
    * 2 client types based on their ability to maintain confidentiality of their client creds:  
        * confidential:  
            * clients capable of maintaining the confidentiality of their creds i.e. client implemented on a secure server.  
        * public:  
            * web-browser based applications etc.  

10. **Oauth2 Client Identifier**
    * The authorization server issues the registered client a client identifier -- a unique string representing the registration information provided by the client.  

11. **OAuth2 Client Authentication**
    * Confidential clients are typically issued (or establish) a set of client credentials used for authenticating with the authorization server (e.g., password, public/private key pair).  
    * **So this is apart from the auth. grant that is issued by the resource owner? And, if yes, then should the client present these creds also (along with the grant) while requesting the auth. server for access token??**  

12. **OAuth2 Client Password**
    * Clients in possession of a client password MAY use the HTTP Basic authentication scheme to authenticate with the auth. server.  
    * The client identifier is encoded using the "application/x-www-form-urlencoded" encoding algorithm and this encoded value is used as the username.  
    * the client pwd is encoded using the same algo and used as the pwd.  
    * The authorization server MUST support the HTTP Basic authentication scheme for authenticating clients that were issued a client password.  
    * So, basically, the identifier becomes the username and the pwd (if any) becomes the password for the client while authenticating with the auth. server for access token request.  
    * **what is http basic authentication??**  
    * **what is application/x-www-form-urlencoded??**  

13. **OAuth2 Protocol Endpoints**
    * There are 2 protocol endpoints:  
        * Auth. endpoint:  
            * used by the client to obtain authorization from the resource owner.  
            * Before this, The authorization server  MUST first verify the identity of the resource owner. The way in which the authorization server authenticates the resource owner (e.g., username and password login, session cookies) is beyond the scope of this specification.  
            * The authorization server MUST support the use of the HTTP "GET" method for the authorization endpoint and MAY support the use of the "POST" method as well.  
            * **but when does this happen in the normal flow? I recall using only token endpoint (fetching access token) and then  using that to access protected resources, so when does the auth. endpoint exactly happen in the examples that I have done so far??**  
        * Token endpoint:  
            * this is used by the client for obtaining an access token by presenting its auth. grant or refresh token.  
            * The token endpoint is used with every authorization grant except for the implicit grant type (since an access token is issued directly).   
            * The client MUST use the HTTP "POST" method when making access token requests.  

14. **OAuth2 Access Token Scope**
    * The authorization and token endpoints allow the client to specify the scope of the access request using the "scope" request parameter.  
    * In turn, the authorization server uses the "scope" response parameter to inform the client of the scope of the access token issued.  
    * The value of the scope parameter is expressed as a list of space-delimited, case-sensitive strings.  
    * The strings are defined by the authorization server.  If the value contains multiple space-delimited strings, their order does not matter.  
    * The authorization server MAY fully or partially ignore the scope requested by the client.  

15. **OAuth2 Issuing an Access Token**
    * If the access token request is valid and authorized, the authorization server issues an access token and optional refresh token.  
    * If the request failed client authentication or is invalid, the authorization server returns an error response.  
    * Successful Response:  
        * access_token:  
            * REQUIRED  
            * The access token issued by the authorization server.  
        * token_type:  
            * REQUIRED  
            * the type of the token issued. value is case insensitive.  
        * expires_in:  
            * RECOMMENDED  
            * The lifetime in seconds of the access token. 
            * If omitted, the authorization server SHOULD provide the expiration time via other means or document the default value.  
        * refresh_token  
            * OPTIONAL  
            * The refresh token, which can be used to obtain new access tokens using the same authorization grant.  
        * scope  
            * OPTIONAL, if identical to the scope requested by the client; 
            * otherwise, REQUIRED.  
    * The parameters are included in the entity-body of the HTTP response using the "application/json" media type.  
    * The client MUST ignore unrecognized value names in the response. 
    * The sizes of tokens and other values received from the authorization server are left undefined. 
    * The client should avoid making assumptions about value sizes. 
    * The authorization server SHOULD document the size of any value it issues.  

16. **OAuth2 Accessing Protected Resources**
    * The client accesses protected resources by presenting the access token to the resource server.  
    * The resource server MUST validate the access token and ensure that it has not expired and that its scope covers the requested resource.  
    * The method in which the client utilizes the access token to authenticate with the resource server depends on the type of access token issued by the authorization server.
    * Typically, it involves using the HTTP "Authorization" request header field [RFC2617] with an authentication scheme defined by the specification of the access token type used.  

17. **OAuth2 Access Token Types**
    * The access token type provides the client with the information required to successfully utilize the access token to make a protected resource request (along with type-specific attributes).  
    * The client MUST NOT use an access token if it does not understand the token type.  
    * For example, 
        * the "bearer" token type defined in [RFC6750] is utilized by simply including the access token string in the request 
        * whereas the "mac" token type defined in [OAuth-HTTP-MAC] is utilized by issuing a Message Authentication Code (MAC) key together with the access token that is used to sign certain components of the HTTP requests.  

18. **OAuth2 Extensibility Options**
    * You can define new Access Token Types, New Endpoint Parameters, New Auth. Grant Types, New Auth. Endpoint Response Types and Additional Error Codes.  
    * Not going into these details.  

19. **OAuth2 Bearer Token**
    * A bearer token is a type of a token issued by the auth. server to the client to access protected resources.  
    * Pure definition: 
        * A security token with the property that any party in possession of the token (a "bearer") can use the token in any way that any other party in possession of it can.     
        * Using a bearer token does not require a bearer to prove possession of cryptographic key material (proof-of-possession).  

20. **OAuth2 Transmitting Bearer Token**
    * There are 3 methods of sending bearer tokens in the resource request to the resource server.  
    * Clients MUST NOT use more than one method to send token in each request.  
    * 3 methods:  
        * Authorization Request Header Field:  
            * the client uses the "Bearer" authentication scheme to transmit the access token in this method.  
        * Form-Encoded Body Parameter:  
            * the client adds the access token to the request-body using the "access_token" parameter but there are many pre-conditions to use this method. 
            * Not going into its detail.  
        * URI Query Parameter:  
            * the client adds the access token to the request URI query component as defined by "Uniform Resource Identifier (URI): Generic Syntax" [RFC3986], using the "access_token" parameter.  
    * **which of these 3 methods have been used in the code examples I have seen so far??** 

21. **OAuth2 Bearer Token Recommendations**
    * Safeguard bearer tokens:  
        * Client implementations MUST ensure that bearer tokens are not leaked to unintended parties, as they will be able to use them to gain access to protected resources.
        * This is the primary security consideration when using bearer tokens and underlies all the more specific recommendations that follow.  
    * Always use TLS (https):  
        * Clients MUST always use TLS [RFC5246] (https) or equivalent transport security when making requests with bearer tokens.  
        * Failing to do so exposes the token to numerous attacks that could give attackers unintended access.  
    * Don't store bearer tokens in cookies:  
        * Implementations MUST NOT store bearer tokens within cookies that can be sent in the clear (which is the default transmission mode for cookies). 
        * Implementations that do store bearer tokens in cookies MUST take precautions against cross-site request forgery.  
    * Issue short-lived bearer tokens:  
        * Token servers SHOULD issue short-lived (one hour or less) bearer tokens, particularly when issuing tokens to clients that run within a web browser or other environments where information leakage may occur. 
        * Using short-lived bearer tokens can reduce the impact of them being leaked.  
    * Issue scoped bearer tokens:  
        * Token servers SHOULD issue bearer tokens that contain an audience restriction, scoping their use to the intended relying party or set of relying parties.  
    * Don't pass bearer tokens in page URLs:  
        * Bearer tokens SHOULD NOT be passed in page URLs (for example, as query string parameters). 
        * Instead, bearer tokens SHOULD be passed in HTTP message headers or message bodies for which confidentiality measures are taken. 
        * Browsers, web servers, and other software may not adequately secure URLs in the browser history, web server logs, and other data structures.  
        * If bearer tokens are passed in page URLs, attackers might be able to steal them from the history data, logs, or other unsecured locations.  
        * **is transmitting bearer token in URI query param not the same as passing in page urls? If yes, then why is even mentioned as one of the ways of transmitting bearer tokens? If no, then what is the diff between these two??**  

22. **JSON Web Token (JWT)**
    * JSON Web Token (JWT) is a compact, URL-safe means of representing claims to be transferred between two parties.  
    * a compact claims representation format intended for space constrained environments such as HTTP Authorization headers and URI query parameters.  
    * JWT claims are encoded in a JSOn Web Signature (JWS) or a JSON Web Encryption (JWE) structure, enabling the claims to be digitally signed or MACed or encrypted.  
    * JWTs represent a set of claims as a JSON object that is encoded in a JWS and/or JWE structure.  This JSON object is the JWT Claims Set.  
    * As per Section 4 of RFC 7159 [RFC7159], 
        * the JSON object consists of zero or more name/value pairs (or members), 
        * where the names are strings and the values are arbitrary JSON values.  
        * These members are the claims represented by the JWT.  
        * The member names within the JWT Claims Set are referred to as Claim Names.  
        * The corresponding values are referred to as Claim Values.  
    * A JWT is represented as a sequence of URL-safe parts separated by period ('.') characters.  
    * Each part contains a base64url-encoded value.  

23. **JSON JWT Example**
    * The following example JOSE Header declares that the encoded object is a JWT, and the JWT is a JWS that is MACed using the HMAC SHA-256 algorithm:  
        *{"typ":"JWT",*    
         *"alg":"HS256"}*    
    * **what is JOSE header?? where can we find in a jwt??**  

24. **JSON JWT Claims**
    * The JWT Claims Set represents a JSON object whose members are the claims conveyed by the JWT.  
    * The Claim Names within a JWT Claims Set MUST be unique.  
    * There are three classes of JWT Claim Names:  
        * Registered Claim Names, 
        * Public Claim Names, and 
        * Private Claim Names. 
        * Not going into its details.  
    * The following is an example of a JWT Claims Set:  
        *{"iss":"joe",*    
        *"exp":1300819380,*    
        *"http://example.com/is_root":true}*    

25. **OAuth2 and JWT**
    * The OAuth 2.0 Authorization Framework [RFC6749] provides a method for making authenticated HTTP requests to a resource using an access token.  
    * Access tokens are issued to third-party clients by an authorization server (AS) with the (sometimes implicit) approval of the resource owner.  
    * In OAuth, an authorization grant is an abstract term used to describe intermediate credentials that represent the resource owner authorization.  
    * An authorization grant is used by the client to obtain an access token.  
    * Several authorization grant types are defined to support a wide range of client types and user experiences.  
    * OAuth also allows for the definition of new extension grant types to support additional clients or to provide a bridge between OAuth and other trust frameworks.  
    * Finally, OAuth allows the definition of additional authentication mechanisms to be used by clients when interacting with the authorization server.  
    * JWT Bearer Token can be used to request an access token and JWT can also be used as a client authentication mechanism.  

26. **Using JWTs as Authorization Grants (OAuth2)**
    * Here is how you can use a Bearer JWT as an authorization grant to request the client for an access token request.  
    * Description of some of the parameters to be used in the access token request with a jwt bearer token auth. grant.  
        * The value of the "grant_type" is "urn:ietf:params:oauth:grant-type:jwt-bearer".  
        * The value of the "assertion" parameter MUST contain a single JWT.  
        * **what is an assertion here??**  
        * The following example demonstrates an access token request with a JWT as an authorization grant (with extra line breaks for display purposes only):  
            *POST /token.oauth2 HTTP/1.1*    
            *Host: as.example.com*    
            *Content-Type: application/x-www-form-urlencoded*    
            *grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer*    
            *&assertion=eyJhbGciOiJFUzI1NiIsImtpZCI6IjE2In0.*    
    * The following examples illustrate what a conforming JWT and an access token request would look like.  
        * The example shows a JWT issued and signed by the system entity identified as "https://jwt-idp.example.com".  
        * The subject of the JWT is identified by email address as "mike@example.com".  
        * The intended audience of the JWT is "https://jwt-rp.example.net", which is an identifier with which the authorization server identifies itself.   
        * The JWT is sent as part of an access token request to the authorization server's token endpoint at "https://authz.example.net/token.oauth2".  
        * Below is the JSON object that could be encoded to produce the JWT Claims Set for a JWT:  
            *{"iss":"https://jwt-idp.example.com",*    
            *"sub":"mailto:mike@example.com",*    
            *"aud":"https://jwt-rp.example.net",*    
            *"nbf":1300815780,*    
            *"exp":1300819380,*    
            *"http://claims.example.com/member":true}*    
    * The following example JSON object, used as the header of a JWT, declares 
        * that the JWT is signed with the Elliptic Curve Digital Signature Algorithm (ECDSA) P-256 SHA-256 
        * using a key identified by the "kid" value "16".  
            *{"alg":"ES256","kid":"16"}*    
    * To present the JWT with the claims and header shown in the previous example as part of an access token request, for example, the client might make the following HTTPS request (with extra line breaks for display purposes only):  
        *POST /token.oauth2 HTTP/1.1*    
        *Host: authz.example.net*    
        *Content-Type: application/x-www-form-urlencoded*    
        *grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer*    
        *&assertion=eyJhbGciOiJFUzI1NiIsImtpZCI6IjE2In0.*    
    * **just not able to relate to or understand where in the example code with jwt has this entire thing come??**        

27. **Using JWTs for Client Authentication (OAuth2)**
    * Not going into its details.  

28. **JWT Format (OAuth2)** 
    * The JWT MUST contain an "iss" (issuer) claim that contains a unique identifier for the entity that issued the JWT.  
    * The JWT MUST contain a "sub" (subject) claim identifying the principal that is the subject of the JWT.  
    * For the authorization grant, the subject typically identifies an authorized accessor for which the access token is being requested  
    * For client authentication, the subject MUST be the "client_id" of the OAuth client.  
    * The JWT MUST contain an "aud" (audience) claim containing a value that identifies the authorization server as an intended audience. The token endpoint URL of the authorization server MAY be used as a value for an "aud" element to identify the authorization server as an intended audience of the JWT.  
    * The JWT MUST contain an "exp" (expiration time) claim that limits the time window during which the JWT can be used. Note that the authorization server may reject JWTs
with an "exp" claim value that is unreasonably far in the future.  
    * There are other optional claims also, not going into those.  
    * The JWT MUST be digitally signed or have a Message Authentication Code (MAC) applied by the issuer.  
    * **again, not sure If I saw any of these in the oauth+jwt+springboot code example??**  

29. **Random Notes on OAuth2, JWT**
    * While a JWT is longer than most access tokens, theyre able to avoid database lookups because the JWT contains a base64 encoded version of the data you need to determine the identity and scope of access.  
    * This is much efficient than looking up an access token in the db to determine who it belongs to and whether it is valid.  
    * Like OAuth access tokens, JWT tokens should be passed in the Authorization header.  
    * The downside of not looking up access tokens with each call is that a JWT cannot be revoked. For that reason, yout require the ability to immediately revoke access.  
    * A few years ago, before the JWT revolution, a <token> was just a string with no intrinsic meaning, e.g. 2pWS6RQmdZpE0TQ93X. That token was then looked-up in a database, which held the claims for that token. The downside of this approach is that DB access (or a cache) is required everytime the token is used.  
    * JWTs encode and verify (via signing) their own claims. This allows folks to issue short-lived JWTs that are stateless (read: self-contained, don't depend on anybody else). They do not need to hit the DB. This reduces DB load and simplifies application architecture.  

30. **OAuth2 Scopes**
    * OAuth 2.0 scopes provide a way to limit the amount of access that is granted to an access token.  
    * For example, an access token issued to a client app may be granted READ and WRITE access to protected resources, or just READ access.  
    * You can implement your APIs to enforce any scope or combination of scopes you wish.  
    * So, if a client receives a token that has READ scope, and it tries to call an API endpoint that requires WRITE access, the call will fail.  
    * You can name your scopes anything you wish. In simple cases, it is fine to use simple names like READ, WRITE, or DELETE. In more complex scenarios where there are multiple API products, each with multiple resources which each support multiple distinct actions, a WRITE on one resource is not equivalent to a WRITE on another resource. In these cases, it's a best practice to assign each scope a unique name, in the form of an URN  


## Notes
1. https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2 - This is a very good listing of all types of grant flows with the url examples.