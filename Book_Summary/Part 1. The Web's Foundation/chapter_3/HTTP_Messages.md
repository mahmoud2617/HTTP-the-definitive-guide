## The Flow of Messages

HTTP messages are the blocks of data sent between HTTP applications. These blocks of data begin with some text meta-information describing the message contents and meaning, followed by optional data. These messages flow between clients, servers, and proxies. The terms ___inbound___, ___outbound___, ___upstream___, and ___downstream___ describe message direction.


### Messages Commute Inbound to the Origin Server:

HTTP uses the terms inbound and outbound to describe transactional direction. Messages travel inbound to the origin server, and when their work is done, they travel outbound back to the user agent.

![[inbound_outbound.png]]


### Messages Flow Downstream:

All messages flow downstream, regardless of whether they are request messages or response messages. The sender of any message is upstream of the receiver.

![[downstream_upstream.png]]


---
---


## The Parts of a Message

HTTP messages are formatted blocks of data. They consist of three parts: a _start line_ describing the message, a block of _headers_ containing attributes, and an optional _body_ containing data.

The start line and headers are just ASCII text, broken up by lines. Each line ends with a two-character end-of-line sequence, consisting of a carriage return and a line-feed character. This end-of-line sequence is written ___CRLF___. It is worth pointing out that while the HTTP specification for terminating lines is ___CRLF___.

The entity body or message body (or just plain “body”) is simply an optional chunk of data. Unlike the start line and headers, the body can contain text or binary data or can be empty.

![[parts_of_message.png]]


### Message Syntax:

All HTTP messages fall into two types: ___request messages___ and ___response messages___. __Request messages__ request an action from a web server. __Response messages__ carry results of a request back to a client.

![[request_response_message.png]]


The format for a request message:
~~~ Markdown
<method> <request-URL> <version>
<headers>

<entity-body>
~~~

The format for a response message:
~~~ Markdown
<version> <status> <reason-phrase>
<headers>

<entity-body>
~~~

![[message_syntax.png]]


__Note__ that a set of HTTP headers should always end in a blank line (bare CRLF), even if there are no headers and even if there is no entity body. Historically, however, many clients and servers (mistakenly) omitted the final CRLF if there was no entity body. To interoperate with these popular but non-compliant implementations, clients and servers should accept messages that end without the final CRLF.


### Start Lines:

#### Request line:

Request messages ask servers to do something to a resource. The start line for a _request message_, or _request line_, contains a method describing what operation the server should perform and a request URL describing the resource on which to perform the method. The request line also includes an HTTP version which tells the server what dialect of HTTP the client is speaking. All of these fields are separated by white-space.

#### Response line:

Response messages carry status information and any resulting data from an operation back to a client. The start line for a _response message_, or _response line_, contains the HTTP version that the response message is using, a numeric status code, and a textual reason phrase describing the status of the operation. All these fields are separated by white-space.

#### Methods:

The method begins the start line of requests, telling the server what to do. The HTTP specifications have defined a set of common request methods.

_Common HTTP methods:_

| Method  | Description                                            | Message body? |
| ------- | ------------------------------------------------------ | ------------- |
| GET     | Get a document from the server.                        | No            |
| HEAD    | Get just the headers for a document from the server.   | No            |
| POST    | Send data to the server for processing.                | Yes           |
| PUT     | Store the body of the request on the server.           | Yes           |
| TRACE   | Trace the message through proxy servers to the server. | No            |
| OPTIONS | Determine what methods can operate on a server.        | No            |
| DELETE  | Remove a document from the server.                     | No            |

Some methods have a body in the request message, and other methods have bodyless requests.

Not all servers implement all seven of the methods. Furthermore, because HTTP was designed to be easily extensible, other servers may implement their own request methods in addition to these. These additional methods are called extension methods, because they extend the HTTP specification.

#### Status codes:

Status codes tell the client what happened. Status codes live in the start lines of responses. For example, in the line `HTTP/1.0 200 OK`, the status code is 200.

Status codes are returned in the start line of each response message. Both a numeric and a human-readable status are returned. The ___numeric code___ makes error processing easy for programs, while the ___reason phrase___ is easily understood by humans.


_Status code classes:_

| Overall range | Defined range | Category      |
| ------------- | ------------- | ------------- |
| 100-199       | 100-101       | Informational |
| 200-299       | 200-206       | Successful    |
| 300-399       | 300-305       | Redirection   |
| 400-499       | 400-415       | Client error  |
| 500-599       | 500-505       | Server error  |

Current versions of HTTP define only a few codes for each status category. As the protocol evolves, more status codes will be defined officially in the HTTP specification. If you receive a status code that you don’t recognize, chances are someone has defined it as an extension to the current protocol. You should treat it as a general member of the class whose range it falls into.

#### Reason phrases:

The reason phrase is the last component of the start line of the response. It provides a textual explanation of the status code. For example, in the line `HTTP/1.0 200 OK`, the reason phrase is __OK__.
The HTTP specification does not provide any hard and fast rules for what reason phrases should look like.

#### Version numbers:

Version numbers appear in both request and response message start lines in the format `HTTP/x.y`. They provide a means for HTTP applications to tell each other what version of the protocol they conform to.

Version numbers are intended to provide applications speaking HTTP with a clue about each other’s capabilities and the format of the message. An HTTP Version 1.2 application communicating with an HTTP Version 1.1 application should know that it should not use any new 1.2 features, as they likely are not implemented by the application speaking the older version of the protocol.


### Headers:

The start line comes a list of zero, one, or many HTTP header fields. HTTP header fields add additional information to request and response messages. They are basically just lists of name/value pairs, e.g. `Content-length: 19`.

#### Header classifications:

___HTTP headers are classified into:___
- _General headers_
	Can appear in both request and response messages
- _Request headers_
	Provide more information about the request
- _Response headers_
	Provide more information about the response
- _Entity headers_
	Describe body size and contents, or the resource itself
- _Extension headers_
	New headers that are not defined in the specification

Each HTTP header has a simple syntax: a name, followed by a colon (:), followed by optional whitespace, followed by the field value, followed by a CRLF.

#### Header continuation lines:

Long header lines can be made more readable by breaking them into multiple lines, preceding each extra line with at least one space or tab character.

_For example:_
~~~ response message
HTTP/1.0 200 OK
Content-Type: image/gif
Content-Length: 8572
Server: Test Server
	Version 1.0
~~~

In this example, the response message contains a Server header whose value is broken into continuation lines. The complete value of the header is `Test Server Version 1.0`.

More information about HTTP headers: [[Appendixes]] -> #HTTP_Header_Reference 


### Entity Bodies:

The third part of an HTTP message is the optional entity body. Entity bodies are the payload of HTTP messages. They are the things that HTTP was designed to transport.

HTTP messages can carry many kinds of digital data: images, video, HTML documents, software applications, credit card transactions, electronic mail, and so on.


---
---


## Methods

### Safe Methods:

HTTP defines a set of methods that are called safe methods. The __GET__ and __HEAD__ methods are said to be safe, meaning that no action should occur as a result of an HTTP request that uses either the __GET__ or __HEAD__ method.
By no action, we mean that nothing will happen on the server as a result of the HTTP request. For example, consider when you are shopping online at Joe’s Hardware and you click on the _submit purchase_ button. Clicking on the button submits a __POST__ request with your credit card information, and an action is performed on the server on your behalf.


### GET:

GET is the most common method. It usually is used to ask a server to send a resource.

![[GET_Method.png]]


### HEAD:

The HEAD method behaves exactly like the GET method, but the server returns only the headers in the response. No entity body is ever returned. This allows a client to inspect the headers for a resource without having to actually get the resource.

Using HEAD, you can: 
- Find out about a resource (e.g., determine its type) without getting it. 
- See if an object exists, by looking at the status code of the response. 
- Test if the resource has been modified, by looking at the headers.

![[HEAD_Method.png]]


### PUT:

The PUT method writes documents to a server, in the inverse of the way that GET reads documents from a server. Some publishing systems let you create web pages and install them directly on a web server using PUT.

![[PUT_Method.png]]

Because PUT allows you to change content, many web servers require you to log in with a password before you can perform a PUT.


### POST:

The POST method was designed to send input data to the server. In practice, it is often used to support HTML forms. The data from a filled-in form typically is sent to the server, which then marshals it off to where it needs to go (e.g., to a server gateway program, which then processes it).

![[POST_Method.png]]

___`POST is used to send data to a server. PUT is used to deposit data into a resource on the server (e.g., a file).`___


### TRACE:

When a client makes a request, that request may have to travel through firewalls, proxies, gateways, or other applications. Each of these has the opportunity to modify the original HTTP request. The TRACE method allows clients to see how its request looks when it finally makes it to the server.

A TRACE request initiates a ___loopback___ diagnostic at the destination server. The server at the final leg of the trip bounces back a TRACE response, with the virgin request message it received in the body of its response. A client can then see how, or if, its original message was munged or modified along the request/response chain of any intervening HTTP applications.

The TRACE method is used primarily for diagnostics; i.e., verifying that requests are going through the request/response chain as intended. It’s also a good tool for seeing the effects of proxies and other applications on your requests.

As good as TRACE is for diagnostics, it does have the drawback of assuming that intervening applications will treat different types of requests (different methods— GET, HEAD, POST, etc.) the same. Many HTTP applications do different things depending on the method—for example, a proxy might pass a POST request directly to the server but attempt to send a GET request to another HTTP application (such as a web cache). TRACE does not provide a mechanism to distinguish methods. Generally, intervening applications make the call as to how they process a TRACE request.

![[TRACE_Method.png]]


### OPTIONS:

The OPTIONS method asks the server to tell us about the various supported capabilities of the web server. You can ask a server about what methods it supports in general or for particular resources. (Some servers may support particular operations only on particular kinds of objects).
This provides a means for client applications to determine how best to access various resources without actually having to access them.

![[OPTIONS_Method.png]]


### DELETE:

The DELETE method asks the server to delete the resources specified by the request URL. However, the client application is not guaranteed that the delete is carried out. This is because the HTTP specification allows the server to override the request without telling the client.

![[DELETE_Method.png]]


### Extension Methods:

HTTP was designed to be field-extensible, so new features wouldn’t cause older software to fail. Extension methods are methods that are not defined in the HTTP/1.1 specification. They provide developers with a means of extending the capabilities of the HTTP services their servers implement on the resources that the servers manage.

_Example web publishing extension methods:_

| Method | Description                                                                                                                                          |
| ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| LOCK   | Allows a user to“lock”a resource—for example, you could lock a resource while you are editing it to prevent others from editing it at the same time. |
| MKCOL  | Allows a user to create a resource.                                                                                                                  |
| COPY   | Facilitates copying resources on a server.                                                                                                           |
| MOVE   | Moves a resource on a server.                                                                                                                        |


---
---


## Status Codes

The status codes provide an easy way for clients to understand the results of their transactions.

### 100–199: Informational Status Codes:

_Informational status codes and reason phrases:_

| Status code | Reason phrase       | Meaning                                                                                                                                                             |
| ----------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 100         | Continue            | Indicates that an initial part of the request was received and the client should continue. After sending this, the server must respond after receiving the request. |
| 101         | Switching Protocols |  Indicates that the server is changing protocols, as specified by the client, to one listed in the Upgrade header.                                                  |

It’s intended to optimize the case where an HTTP client application has an entity body to send to a server but wants to check that the server will accept the entity before it sends it.

#### Clients and 100 Continue:

If a client is sending an entity to a server and is willing to wait for a 100 Continue response before it sends the entity, the client needs to send an Expect request header with the value 100-continue. If the client is not sending an entity, it shouldn’t send a 100-continue Expect header, because this will only confuse the server into thinking that the client might be sending an entity.

A client application should really use 100-continue only to avoid sending a server a large entity that the server will not be able to handle or use.

Clients that send an Expect header for 100- continue should not wait forever for the server to send a 100 Continue response. After some timeout, the client should just send the entity.

In practice, client implementors also should be prepared to deal with unexpected 100 Continue responses. Some errant HTTP applications send this code inappropriately.

#### Servers and 100 Continue:

If a server receives a request with the Expect header and 100-continue value, it should respond with either the 100 Continue response or an error code. Servers should never send a 100 Continue status code to clients that do not send the 100- continue expectation. However, some errant servers do this.

If for some reason the server receives some (or all) of the entity before it has had a chance to send a 100 Continue response, it does not need to send this status code, because the client already has decided to continue.

If a server receives a request with a 100-continue expectation and it decides to end the request before it has read the entity body (e.g., because an error has occurred), it should not just send a response and close the connection, as this can prevent the client from receiving the response.

#### Proxies and 100 Continue:

A proxy that receives from a client a request that contains the 100-continue expectation needs to do a few things. If the proxy either knows that the next-hop server is HTTP/1.1-compliant or does not know what version the next-hop server is compliant with, it should forward the request with the Expect header in it. If it knows that the next-hop server is compliant with a version of HTTP earlier than 1.1, it should respond with the 417 Expectation Failed error.

If a proxy decides to include an Expect header and 100-continue value in its request on behalf of a client that is compliant with HTTP/1.0 or earlier, it should not forward the 100 Continue response (if it receives one from the server) to the client, because the client won’t know what to make of it.


### 200–299: Success Status Codes:

When clients make requests, the requests usually are successful. Servers have an array of status codes to indicate success, matched up with different types of requests.

_Success status codes and reason phrases:_

| Status code | Reason phrase                 | Meaning                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ----------- | ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 200         | OK                            | Request is okay, entity body contains requested resource.                                                                                                                                                                                                                                                                                                                                                                                                             |
| 201         | Created                       | For requests that create server objects (e.g., PUT). The entity body of the response should contain the various URLs for referencing the created resource, with the Location header containing the most specific reference.<br>The server must have created the object prior to sending this status code.                                                                                                                                                             |
| 202         | Accepted                      | The request was accepted, but the server has not yet performed any action with it. There are no guarantees that the server will complete the request; this just means that the request looked valid when accepted.<br>The server should include an entity body with a description indicating the status of the request and possibly an estimate for when it will be completed or a pointer to where this information can be obtained.                                 |
| 203         | Non-Authoritative Information | The information contained in the entity headers came not from the origin server but from a copy of the resource. This could happen if an intermediary had a copy of a resource but could not or did not validate the meta-information (headers) it sent about the resource.<br>This response code is not required to be used; it is an option for applications that have a response that would be a 200 status if the entity headers had come from the origin server. |
| 204         | No Content                    | The response message contains headers and a status line, but no entity body. Primarily used to update browsers without having them move to a new document (e.g., refreshing a form page).                                                                                                                                                                                                                                                                             |
| 205         | Reset Content                 | Another code primarily for browsers. Tells the browser to clear any HTML form elements on the current page.                                                                                                                                                                                                                                                                                                                                                           |
| 206         | Partial Content               | A partial or range request was successful. This status code indicates that the range request was successful.<br>A 206 response must include a Content-Range, Date, and either `ETag` or `ContentLocation` header.                                                                                                                                                                                                                                                     |


### 300–399: Redirection Status Codes:

The redirection status codes either tell clients to use alternate locations for the resources they’re interested in or provide an alternate response instead of the content. If a resource has moved, a redirection status code and an optional Location header can be sent to tell the client that the resource has moved and where it can now be found.

![[redirection.png]]

Some of the redirection status codes can be used to validate an application’s local copy of a resource with the origin server.

![[validate_local_cache.png]]

_Redirection status codes and reason phrases:_

| Status code | Reason phrase      | Meaning                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ----------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 300         | Multiple Choices   | Returned when a client has requested a URL that actually refers to multiple resources, such as a server hosting an English and French version of an HTML document. This code is returned along with a list of options; the user can then select which one he wants. The server can include the preferred URL in the Location header.                                                                                                                                         |
| 301         | Moved Permanently  | Used when the requested URL has been moved. The response should contain in the Location header the URL where the resource now resides.                                                                                                                                                                                                                                                                                                                                       |
| 302         | Found              | Like the 301 status code; however, the client should use the URL given in the Location header to locate the resource temporarily. Future requests should use the old URL.                                                                                                                                                                                                                                                                                                    |
| 303         | See Other          | Used to tell the client that the resource should be fetched using a different URL. This new URL is in the Location header of the response message. Its main purpose is to allow responses to POST requests to direct a client to a resource.                                                                                                                                                                                                                                 |
| 304         | Not Modified       | Clients can make their requests conditional by the request headers they include. If a client makes a conditional request, such as a GET if the resource has not been changed recently, this code is used to indicate that the resource has not changed. Responses with this status code should not contain an entity body.                                                                                                                                                   |
| 305         | Use Proxy          | Used to indicate that the resource must be accessed through a proxy; the location of the proxy is given in the Location header. It’s important that clients interpret this response relative to a specific resource and do not assume that this proxy should be used for all requests or even all requests to the server holding the requested resource. This could lead to broken behavior if the proxy mistakenly interfered with a request, and it poses a security hole. |
| 306         | (Unused)           | Not currently used.                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| 307         | Temporary Redirect | Like the 301 status code; however, the client should use the URL given in the Location header to locate the resource temporarily. Future requests should use the old URL.                                                                                                                                                                                                                                                                                                    |

When an `HTTP/1.0` client makes a POST request and receives a 302 redirect status code in response, it will follow the redirect URL in the Location header with a GET request to that URL (instead of making a POST request, as it did in the original request).
`HTTP/1.0` servers expect `HTTP/1.0` clients to do this—when an `HTTP/1.0` server sends a 302 status code after receiving a POST request from an `HTTP/1.0` client, the server expects that client to follow the redirect with a GET request to the redirected URL.

The confusion comes in with `HTTP/1.1`. The `HTTP/1.1` specification uses the 303 status code to get this same behavior (servers send the 303 status code to redirect a client’s POST request to be followed with a GET request).
To get around the confusion, the `HTTP/1.1` specification says to use the 307 status code in place of the 302 status code for temporary redirects to `HTTP/1.1` clients. Servers can then save the 302 status code for use with `HTTP/1.0` clients.


### 400–499: Client Error Status Codes:

_Client error status codes and reason phrases:_

| Status code | Reason phrase                   | Meaning                                                                                                                                                                                                                                                                                                  |
| ----------- | ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 400         | Bad Request                     | Used to tell the client that it has sent a malformed request.                                                                                                                                                                                                                                            |
| 401         | Unauthorized                    | Returned along with appropriate headers that ask the client to authenticate itself before it can gain access to the resource.                                                                                                                                                                            |
| 402         | Payment Required                | Currently this status code is not used, but it has been set aside for future use.                                                                                                                                                                                                                        |
| 403         | Forbidden                       | Used to indicate that the request was refused by the server. If the server wants to indicate why the request was denied, it can include an entity body describing the reason. However, this code usually is used when the server does not want to reveal the reason for the refusal.                     |
| 404         | Not Found                       | Used to indicate that the server cannot find the requested URL. Often, an entity is included for the client application to display to the user.                                                                                                                                                          |
| 405         | Method Not Allowed              | Used when a request is made with a method that is not supported for the requested URL. The Allow header should be included in the response to tell the client what methods are allowed on the requested resource.                                                                                        |
| 406         | Not Acceptable                  | Clients can specify parameters about what types of entities they are willing to accept. This code is used when the server has no resource matching the URL that is acceptable for the client. Often, servers include headers that allow the client to figure out why the request could not be satisfied. |
| 407         | Proxy Authentication Required   | Like the 401 status code, but used for proxy servers that require authentication for a resource.                                                                                                                                                                                                         |
| 408         | Request Timeout                 | If a client takes too long to complete its request, a server can send back this status code and close down the connection. The length of this timeout varies from server to server but generally is long enough to accommodate any legitimate request.                                                   |
| 409         | Conflict                        | Used to indicate some conflict that the request may be causing on a resource. Servers might send this code when they fear that a request could cause a conflict. The response should contain a body describing the conflict.                                                                             |
| 410         | Gone                            | Similar to 404, except that the server once held the resource. Used mostly for web site maintenance, so a server’s administrator can notify clients when a resource has been removed.                                                                                                                    |
| 411         | Length Required                 | Used when the server requires a Content-Length header in the request message.                                                                                                                                                                                                                            |
| 412         | Precondition Failed             | Used if a client makes a conditional request and one of the conditions fails. Conditional requests occur when a client includes an Expect header.                                                                                                                                                        |
| 413         | Request Entity Too Large        | Used when a client sends an entity body that is larger than the server can or wants to process.                                                                                                                                                                                                          |
| 414         | Request URI Too Long            | Used when a client sends a request with a request URL that is larger than the server can or wants to process.                                                                                                                                                                                            |
| 415         | Unsupported Media Type          | Used when a client sends an entity of a content type that the server does not understand or support.                                                                                                                                                                                                     |
| 416         | Requested Range Not Satisfiable | Used when the request message requested a range of a given resource and that range either was invalid or could not be met.                                                                                                                                                                               |
| 417         | Expectation Failed              | Used when the request contained an expectation in the Expect request header that the server could not satisfy.<br>A proxy or other intermediary application can send this response code if it has unambiguous evidence that the origin server will generate a failed expectation for the request.        |


### 500–599: Server Error Status Codes:

_Server error status codes and reason phrases:_

| Status code | Reason phrase              | Meaning                                                                                                                                                                                                                    |
| ----------- | -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 500         | Internal Server Error      | Used when the server encounters an error that prevents it from servicing the request.                                                                                                                                      |
| 501         | Not Implemented            | Used when a client makes a request that is beyond the server’s capabilities (e.g., using a request method that the server does not support).                                                                               |
| 502         | Bad Gateway                | Used when a server acting as a proxy or gateway encounters a bogus response from the next link in the request response chain (e.g., if it is unable to connect to its parent gateway).                                     |
| 503         | Service Unavailable        | Used to indicate that the server currently cannot service the request but will be able to in the future. If the server knows when the resource will become available, it can include a Retry-After header in the response. |
| 504         | Gateway Timeout            | Similar to status code 408, except that the response is coming from a gateway or proxy that has timed out waiting for a response to its request from another server.                                                       |
| 505         | HTTP Version Not Supported | Used when a server receives a request in a version of the protocol that it can’t or won’t support. Some server applications elect not to support older versions of the protocol.                                           |

---
---


## Headers

### General Headers:

_General informational headers:_

| Header            | Description                                                                                               |
| ----------------- | --------------------------------------------------------------------------------------------------------- |
| Connection        | Allows clients and servers to specify options about the request/response connection.                      |
| Date              | Provides a date and time stamp telling when the message was created.                                      |
| MIME-Version      | Gives the version of MIME that the sender is using.                                                       |
| Trailer           | Lists the set of headers that are in the trailer of a message encoded with the chunked transfer encoding. |
| Transfer-Encoding | Tells the receiver what encoding was performed on the message in order for it to be transported safely.   |
| Upgrade           | Gives a new version or protocol that the sender would like to __upgrade__ to using.                       |
| Via               | Shows what intermediaries (proxies, gateways) the message has gone through.                               |

#### General caching headers:

`HTTP/1.0` introduced the first headers that allowed HTTP applications to cache local copies of objects instead of always fetching them directly from the origin server.


_Basic general caching headers:_

| Header        | Description                                                                            |
| ------------- | -------------------------------------------------------------------------------------- |
| Cache-Control | Used to pass caching directions along with the message.                                |
| Pragma        | Another way to pass directions along with the message, though not specific to caching. |


### Request Headers:

_Request informational headers:_

| Header     | Description                                                                        |
| ---------- | ---------------------------------------------------------------------------------- |
| Client-IP  | Provides the IP address of the machine on which the client is running.             |
| From       | Provides the email address of the client’s user.                                   |
| Host       | Gives the hostname and port of the server to which the request is being sent.      |
| Referer    | Provides the URL of the document that contains the current request URI.            |
| UA-Color   | Provides information about the color capabilities of the client machine’s display. |
| UA-CPU     | Gives the type or manufacturer of the client’s CPU.                                |
| UA-Disp    | Provides information about the client’s display screen capabilities.               |
| UA-OS      | Gives the name and version of operating system running on the client machine.      |
| UA-Pixels  | Provides pixel information about the client machine’s display.                     |
| User-Agent | Tells the server the name of the application making the request.                   |

Client-IP and the ___UA-*___ headers are not defined in _RFC 2616_ but are implemented by many HTTP client applications.
While implemented by some clients, the ___UA-*___ headers can be considered harmful. Content, specifically HTML, should not be targeted at specific client configurations.

#### Accept headers:

Accept headers benefit both sides of the connection. Clients get what they want, and servers don’t waste their time and bandwidth sending something the client can’t use.

_Accept headers:_

| Header          | Description                                                       |
| --------------- | ----------------------------------------------------------------- |
| Accept          | Tells the server what media types are okay to send.               |
| Accept-Charset  | Tells the server what charsets are okay to send.                  |
| Accept-Encoding | Tells the server what encodings are okay to send.                 |
| Accept-Language | Tells the server what languages are okay to send.                 |
| TE              | Tells the server what extension transfer codings are okay to use. |

#### Conditional request headers:

Using conditional request headers, clients can put such restrictions on requests, requiring the server to make sure that the conditions are true before satisfying the request.

_Conditional request headers:_

| Header              | Description                                                                               |
| ------------------- | ----------------------------------------------------------------------------------------- |
| Expect              | Allows a client to list server behaviors that it requires for a request.                  |
| If-Match            | Gets the document if the entity tag matches the current entity tag for the document.      |
| If-Modified-Since   | Restricts the request unless the resource has been modified since the specified date.     |
| If-None-Match       | Gets the document if the entity tags supplied do not match those of the current document. |
| If-Range            | Allows a conditional request for a range of a document.                                   |
| If-Unmodified-Since | Restricts the request unless the resource has not been modified since the specified date. |
| Range               | Requests a specific range of a resource, if the server supports range requests.           |

#### Request security headers:

_Request security headers:_

| Header        | Description                                                                                                           |
| ------------- | --------------------------------------------------------------------------------------------------------------------- |
| Authorization | Contains the data the client is supplying to the server to authenticate itself.                                       |
| Cookie        | Used by clients to pass a token to the server.<br>Not a true security header, but it does have security implications. |
| Cookie2       | Used to note the version of cookies a requestor supports.                                                             |

#### Proxy request headers:

As proxies become increasingly common on the Internet, a few headers have been defined to help them function better.

_Proxy request headers:_

| Header              | Description                                                                                                                                           |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| Max-Forwards        | The maximum number of times a request should be forwarded to another proxy or gateway on its way to the origin server.<br>Used with the TRACE method. |
| Proxy-Authorization | Same as Authorization, but used when authenticating with a proxy.                                                                                     |
| Proxy-Connection    | Same as Connection, but used when establishing connections with a proxy.                                                                              |


### Response Headers:

_Response informational headers:_

| Header      | Description                                                         |
| ----------- | ------------------------------------------------------------------- |
| Age         | How old the response is.                                            |
| Public      | A list of request methods the server supports for its resources.    |
| Retry-After | A date or time to try back, if a resource is unavailable.           |
| Server      | The name and version of the server’s application software.          |
| Title       | For HTML documents, the title as given by the HTML document source. |
| Warning     | A more detailed warning message than what is in the reason phrase.  |

#### Negotiation headers:

`HTTP/1.1` provides servers and clients with the ability to negotiate for a resource if multiple representations are available, e.g. when there are both French and German translations of an HTML document on a server.


_Negotiation headers:_

| Header        | Description                                                                                                                                                                                              |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Accept-Ranges | The type of ranges that a server will accept for this resource.                                                                                                                                          |
| Vary          | A list of other headers that the server looks at and that may cause the response to vary, i.e. a list of headers the server looks at to pick which is the best version of a resource to send the client. |

#### Response security headers:

_Response security headers:_

| Header             | Description                                                                                                                                             |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Proxy-Authenticate | A list of challenges for the client from the proxy.                                                                                                     |
| Set-Cookie         | Not a true security header, but it has security implications.<br>Used to set a token on the client side that the server can use to identify the client. |
| Set-Cookie2        | Similar to Set-Cookie.                                                                                                                                  |
| WWW-Authenticate   | A list of challenges for the client from the server.                                                                                                    |


### Entity Headers:

There are many headers to describe the payload of HTTP messages. Because both request and response messages can contain entities, these headers can appear in either type of message.
In general, entity headers tell the receiver of the message what it’s dealing with.


_Entity informational headers:_

| Header   | Description                                                                                                                                   |
| -------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Allow    | Lists the request methods that can be performed on this entity.                                                                               |
| Location | Tells the client where the entity really is located.<br>Used in directing the receiver to a "possibly new" location __URL__ for the resource. |

#### Content headers:

The content headers provide specific information about the content of the entity, revealing its type, size, and other information useful for processing it.


_Content headers:_

| Header           | Description                                                              |
| ---------------- | ------------------------------------------------------------------------ |
| Content-Base     | The base URL for resolving relative URLs within the body.                |
| Content-Encoding | Any encoding that was performed on the body.                             |
| Content-Language | The natural language that is best used to understand the body.           |
| Content-Length   | The length or size of the body.                                          |
| Content-Location | Where the resource actually is located.                                  |
| Content-MD5      | An MD5 checksum of the body.                                             |
| Content-Range    | The range of bytes that this entity represents from the entire resource. |
| Content-Type     | The type of object that this body is.                                    |

#### Entity caching headers:

The general caching headers provide directives about how or when to cache. The entity caching headers provide information about the entity being cached. e.g. information needed to validate whether a cached copy of the resource is still valid and hints about how better to estimate when a cached resource may no longer be valid.


_Entity caching headers:_

| Header        | Description                                                                                                          |
| ------------- | -------------------------------------------------------------------------------------------------------------------- |
| ETag          | The entity tag associated with this entity.                                                                          |
| Expires       | The date and time at which this entity will no longer be valid and will need to be fetched from the original source. |
| Last-Modified |  The last date and time when this entity changed.                                                                    |

Entity tags are basically identifiers for a particular version of a resource.


More information about HTTP headers: [[Appendixes]] -> #HTTP_Header_Reference 


---
---


## Done.
---
---

> ___تم بحمد الله 3>___

---
---
