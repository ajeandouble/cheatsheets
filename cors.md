# CORS

## Notes

## Resources

[Hacking HTTP CORS from Inside Out](https://infosecwriteups.com/hacking-http-cors-from-inside-out-512cb125c528)

## Misc

What are preflight requests in cors

Preflight requests are a type of HTTP request that are sent by the browser before a main request is made. They are used to check if the main request is safe to send and to determine if the server will allow the main request to be sent. Preflight requests are used when a main request might have unintended side effects or if it is not a simple request, as defined by the CORS (Cross-Origin Resource Sharing) specification.

In a preflight request, the browser sends an HTTP OPTIONS request to the server to determine if the actual request is safe to send. The server then responds with information about what methods and headers are allowed for the actual request. If the server allows the actual request to be made, it sends back an HTTP status code of 200 (OK). If the server does not allow the request to be made, it sends back an HTTP status code of 403 (Forbidden).

Preflight requests are a security measure that help to prevent malicious websites from making unauthorized requests to other sites on behalf of the user. They are an important part of the CORS specification, which is a mechanism that allows web pages on different domains to communicate with each other in a secure and controlled manner.





Give me an example of a preflight request http packet
Here is an example of an HTTP preflight request packet:

Copy code
OPTIONS /resource/123 HTTP/1.1
Host: example.com
Connection: keep-alive
Access-Control-Request-Method: POST
Access-Control-Request-Headers: origin, content-type
Origin: https://mywebsite.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.66 Safari/537.36
Accept: */*
Referer: https://mywebsite.com/
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
This preflight request is asking the server at example.com if it is allowed to make a POST request to the /resource/123 endpoint, with the origin and content-type headers. The Origin header specifies the domain of the website making the request (https://mywebsite.com), and the Access-Control-Request-Method and Access-Control-Request-Headers headers specify the method and headers that will be used in the actual request.

The server will then respond with information about what methods and headers are allowed for the actual request. If the server allows the actual request to be made, it will send back an HTTP status code of 200 (OK) along with the appropriate Access-Control-Allow-* headers. If the server does not allow the request to be made, it will send back an HTTP status code of 403 (Forbidden).





do the access-control-request-method and access-control-request-headers headers are still present on other packets sent later
No, the Access-Control-Request-Method and Access-Control-Request-Headers headers are only present in the preflight request. They are not included in any subsequent requests.

The preflight request is a separate HTTP request that is sent by the browser before the actual request, in order to check if the server will allow the actual request to be made. If the server allows the actual request to be made, it sends back an HTTP status code of 200 (OK) along with the appropriate Access-Control-Allow-* headers. The browser then proceeds to make the actual request, which does not include the Access-Control-Request-Method and Access-Control-Request-Headers headers.

For example, if the preflight request is asking the server if it is allowed to make a POST request to the /resource/123 endpoint, the actual POST request would look like this:

Copy code
POST /resource/123 HTTP/1.1
Host: example.com
Connection: keep-alive
Content-Type: application/json
Origin: https://mywebsite.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.66 Safari/537.36
Accept: */*
Referer: https://mywebsite.com/
Content-Length: 123
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9

{
  "key": "value"
}
As you can see, the Access-Control-Request-Method and Access-Control-Request-Headers headers are not present in the actual POST request. They are only used in the preflight request.





So cors is enforced only by the browser? Let's say I forge an http request without any web browser then the server won't care about which domain I'm sending the request from?
Yes, that's correct. CORS (Cross-Origin Resource Sharing) is a mechanism that is implemented by web browsers to enforce security restrictions on HTTP requests made from one domain to another. If you make an HTTP request directly, without going through a web browser, then the browser's CORS enforcement mechanisms will not be triggered, and the request will not be subject to CORS restrictions.

This means that if you make an HTTP request from a server or script, without going through a web browser, the server will not care about the origin of the request, and it will not enforce any CORS restrictions. The server will simply treat the request as a normal HTTP request, and it will either process the request or respond with an appropriate HTTP error code.

It is important to note that CORS is just one mechanism that is used to enforce security restrictions on HTTP requests. There are other mechanisms, such as the Same-Origin Policy and Content Security Policy, that can also be used to enforce security restrictions on HTTP requests. These mechanisms are also implemented by web browsers and are not triggered by HTTP requests made directly from servers or scripts.





What is the different between CORS allowed origins and CSFR allowed origins and CSRF related policies?
CORS (Cross-Origin Resource Sharing) is a mechanism that allows web pages on different domains to communicate with each other in a secure and controlled manner. It is implemented by web browsers, and it allows a server to specify which origins are allowed to make HTTP requests to it.

An "origin" in this context refers to the combination of a domain, protocol, and port number. For example, https://www.example.com and https://api.example.com are considered to be different origins, even though they are both on the same domain (example.com).

CORS is used to allow web pages on one origin to make HTTP requests to a server on a different origin, but only if the server specifically allows it. The server can specify which origins are allowed to make HTTP requests to it by setting the Access-Control-Allow-Origin header in its responses. For example, if the server sets the Access-Control-Allow-Origin header to https://www.example.com, then web pages on https://www.example.com will be allowed to make HTTP requests to the server, but web pages on other origins will not.

CSRF (Cross-Site Request Forgery) is a type of attack that involves tricking a user into making an unintended HTTP request to a server, usually by exploiting the user's authenticated session on the server. CSRF attacks can be prevented by implementing various security measures, such as requiring that all requests include a unique token that is checked by the server.

The "allowed origins" for CORS and CSRF are different concepts. CORS allowed origins refer to the domains that are allowed to make HTTP requests to a server, as specified by the server using the Access-Control-Allow-Origin header. CSRF allowed origins refer to the domains that are trusted to make HTTP requests on behalf of the user, as specified by the server using various security measures, such as unique tokens or same-site cookies.

CORS and CSRF are both security mechanisms that are used to protect against different types of attacks. CORS is used to protect against cross-origin attacks, where an attacker tries to make unauthorized requests to a server from a different domain. CSRF is used to protect against cross-site attacks, where an attacker tries to trick a user into making unintended requests to a server.





What exactly is a cross site attack?
A cross-site attack (also known as a cross-site request forgery, or CSRF) is a type of attack that involves tricking a user into making an unintended HTTP request to a server, usually by exploiting the user's authenticated session on the server.

In a cross-site attack, the attacker creates a malicious web page or email that contains a link or form that is designed to send an HTTP request to a server when the user clicks on it or submits the form. The request is made as if it were coming from the user, so the server will process the request and apply any changes or actions as if they were requested by the user.

For example, consider a situation where a user is logged into a website that allows them to transfer money between accounts. If the user is tricked into clicking on a link or submitting a form that is crafted by an attacker, the request could transfer money out of the user's account without their knowledge. This is a simple example of a cross-site attack.

Cross-site attacks can be prevented by implementing various security measures on the server, such as requiring that all requests include a unique token that is checked by the server, or by using same-site cookies to ensure that requests are only accepted if they come from the same domain as the server.





Yeah but if the users click on a link that is on the right website that consumes the API. How does it prevent the user for still appearing as willingly wanting to do the transfer?
If the user is authenticated on the website and clicks on a link or submits a form that is on the same domain as the server, then the server will process the request as if it were a normal and intended request from the user. In this case, the server would not be able to distinguish between a legitimate request from the user and a cross-site attack, because both types of requests would appear to come from the same domain and would be accompanied by the user's authenticated session.

To prevent this type of attack, the server can implement various security measures to ensure that requests are only accepted if they are genuinely initiated by the user. One common approach is to use unique tokens that are checked by the server on each request.

For example, the server could generate a unique token and include it as a hidden field in a form that the user needs to submit. When the user submits the form, the server will check the token to make sure it is valid. If the token is valid, the server will process the request. If the token is not valid, the server will reject the request as an attempted cross-site attack.

This approach helps to prevent cross-site attacks because it ensures that requests can only be made if they include a valid token. An attacker would not be able to craft a malicious request that includes a valid token, because the attacker does not have access to the token. This makes it much more difficult for an attacker to successfully carry out a cross-site attack.





So CSRF are on forms? That's why you have to put them in django template forms for them to work?
Yes, CSRF (Cross-Site Request Forgery) attacks often involve the use of forms. This is because forms are a common way for users to interact with websites and make requests to servers.

In a CSRF attack, the attacker creates a malicious web page or email that contains a form that is designed to send an HTTP request to a server when the user submits the form. The request is made as if it were coming from the user, so the server will process the request and apply any changes or actions as if they were requested by the user.

To protect against CSRF attacks, it is common to use unique tokens that are checked by the server on each request. One way to do this is to include a unique token as a hidden field in the form. When the user submits the form, the server will check the token to make sure it is valid. If the token is valid, the server will process the request. If the token is not valid, the server will reject the request as an attempted CSRF attack.

In Django, this can be done by using the {% csrf_token %} template tag in your form templates. This will automatically insert a hidden field in the form that contains a unique token. When the form is submitted, Django will check the token to make sure it is valid, and it will reject the request if the token is not valid. This helps to protect against CSRF attacks by ensuring that requests can only be made if they include a valid token.
