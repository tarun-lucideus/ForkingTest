	
# Autocomplete Enabled
> **Vulnerability ID:** `LWV <control-id>`
> **Control Group:** `<control-group>`
> **Tentative Severity:** `severity`


## Description
Authenticated session cookies must have HttpOnly attribute set to prevent cookie access through scripts. The application does not set HTTPOnly flag on the session cookie being used.

## Impact
Lack of HttpOnly flag on a session cookies allows javascript to access it. Malicious javascript inserted by an attacker can give them access to the authenticated session cookie thus resulting in session hijacking and complete compromise of the victim's account.

### Technical Impact
Lack of HttpOnly flag on a session cookies allows javascript to access it. Malicious javascript inserted by an attacker can give them access to the authenticated session cookie thus resulting in session hijacking and complete compromise of the victim's account.

### Business Impact
If HttpOnly flag is not set on the session cookies then an attacker can access the session cookies of the victim and can hijack the session of the victim by injecting the malicious javascript payloads if application is vulnerable to cross site scripting.

## Recommendations
Session Cookies must have HttpOnly attribute to prevent cookie access from client-side javascript.

### PHP
Authenticated session cookies must have HttpOnly attribute set to prevent cookie access through scripts.
Following should be done to set the HttpOnly flag on session cookie to prevent it from being accessed through client side scripts

a.)For session cookies managed by PHP, the flag is set permanently in php.in through the parameter:
session.cookie_httponly = True

or in and during a script via the function:
void session_set_cookie_params ( int $lifetime [, string $path [, string $domain [, bool $secure= true [, bool $httponly= true ]]]] )

b.)For application cookies last parameter in setcookie() sets HttpOnly flag
bool setcookie  ( string $name  [, string $value  [, int $expire= 0  [, string $path  
                 [, string $domain  [, bool $secure= true  [, bool $httponly= true  ]]]]]] )

### .NET
"Following code can be used to set the HttpOnly flag on session cookie:

// Setting the HttpOnly value to true makes it available only to ASP.Net

mysessionCookie.HttpOnly = true;

The same can also be configured in root web.config in system.web:

<system.web>
  <httpCookies httpOnlyCookies=""true"" lockItem=""true"" />
</system.web>"

### Java
Following steps can be followed to set the HttpOnly flag on session cookie:

For JEE6 and above, setHttpOnly and isHttpOnly methods are available in the Cookie interface, and also for session cookies (JSESSIONID):
 
 Cookie cookie = getMyCookie(""myCookieName"");
 cookie.setHttpOnly(true);
 
The following configuration can also be applied for the same in the deployment descriptor WEB-INF/web.xml:
 
 <session-config>
  <cookie-config>
  <http-only>true</http-only>
  </cookie-config>
 </session-config>
 
For JEE versions prior to JEE 6 a common workaround is to overwrite the SET-COOKIE http response header with a session cookie value that explicitly appends the HttpOnly flag:
 
 String sessionid = request.getSession().getId();
 response.setHeader(""SET-COOKIE"", ""JSESSIONID="" + sessionid + ""; HttpOnly"");

Care should be taken that other flags appended to the cookie are not overwritten while following the above steps.



## Classification
Broken Authentication and Session Management

## References
General References goes here

### PHP
Reference: https://www.owasp.org/index.php/HttpOnly#Using_PHP_to_set_HttpOnly

### .NET
Reference: https://msdn.microsoft.com/en-us/library/system.web.httpcookie.httponly(v=vs.110).aspx?cs-save-lang=1&cs-lang=csharp#code-snippet-2

### JAVA
Reference: http://stackoverflow.com/questions/15510354/how-to-set-httponly-and-session-cookie-for-java-web-appliaction

