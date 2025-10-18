## HTTP: The Internet's Multimedia Courier:

Because HTTP uses reliable data-transmission protocols, it's guarantees that your data will not be damaged or scrambled in transit, even when it comes from other side of the globe.

---

## Web Clients and Servers:

The **_Web servers_** (aka **_HTTP servers_**) store the internet's data and provide the data when it's requested by HTTP clients. The clients send HTTP requests to servers and servers return the requested data in HTTP responses.

![[web_client_and_servers.png]]

---

## Resources:

Web servers host ___web resources___. A web resource is the source of web content. The simplest kind of web resource is a static file on the web server's file-system. These files can contain anything: they might be text files, HTML files, Microsoft Word files, Adobe Acrobat files, JPEG image files, AVI movie files, or any other format.

Resources can also be software programs that generate content on demand. These dynamic content resources can generate content based on your identity, on what information you’ve requested, or on the time of day. They can show you a live image from a camera, or let you trade stocks, search real estate databases, or buy gifts from online stores.

![[web_resources.png]]

---

## Media Types:

Because the Internet hosts many thousands of different data types, HTTP carefully tags each object being transported through the Web with a data format label called a ___MIME___ type. __MIME__ (_Multipurpose Internet Mail Extensions_) was originally designed to solve problems encountered in moving messages between different electronic mail systems.

Web servers attach a MIME type to all HTTP object data. When a web browser gets an object back from a server, it looks at the associated MIME type to see if it knows how to handle the object. Most browsers can handle hundreds of popular object types: displaying image files, parsing and formatting HTML files, playing audio files through the computer’s speakers, or launching external plug-in software to handle special formats.

![[media_types.png]]

A MIME type is a textual label, represented as a ___primary object type___ and a specific ___subtype___, separated by a slash. _For example_: 
- An HTML-formatted text document would be labeled with type _text/html_.
- A plain ASCII text document would be labeled with type _text/plain_.
- A JPEG version of an image would be _image/jpeg_.
- A GIF-format image would be _image/gif_.
- An Apple QuickTime movie would be _video/quicktime_.
- A Microsoft PowerPoint presentation would be _application/vnd.ms-powerpoint_.

---

## URIs:

Each web server resource has a name, so clients can point out what resources they are interested in. The server resource name is called a ___uniform resource identifier___, or __URI__. URIs are like the postal addresses of the Internet, uniquely identifying and locating information resources around the world.

_For example:_ http://www.joes-hardware.com/specials/saw-blade.gif

URIs come in two flavors, called URLs and URNs.

---

## URLs:

The ___uniform resource locator___ (__URL__) is the most common form of resource identifier. URLs describe the specific location of a resource on a particular server. They tell you exactly how to fetch a resource from a precise, fixed location.

![[URLs.png]]


___Example URLs:___

| URL                                                         | Description                                                                                        |
| ----------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| http://www.oreilly.com/index.html                           | The home URL for O’Reilly & Associates, Inc.                                                       |
| http://www.yahoo.com/images/logo.gif                        | The URL for the Yahoo! web site’s logo.                                                            |
| http://www.joes-hardware.com/inventory-check.cgi?item=12731 | The URL for a program that checks if inventory item #12731 is in stock.                            |
| ftp://joe:tools4u@ftp.joes-hardware.com/lockingpliers.gif   | The URL for thelocking-pliers.gif image file, using password-protected FTP as the access protocol. |

Most URLs follow a standardized format of three main parts:
- The first part of the URL is called the ___scheme___, and it describes the protocol used to access the resource. This is usually the HTTP protocol (http://).
- The second part gives the server Internet address (e.g., www.joes-hardware.com).
- The rest names a resource on the web server (e.g., /specials/saw-blade.gif).

___Almost every URI is a URL.___

---

## URNs:

A ___uniform resource name___ (__URN__) serves as a unique name for a particular piece of content, independent of where the resource currently resides. These location-independent URNs allow resources to move from place to place. URNs also allow resources to be accessed by multiple network access protocols while maintaining the same name.

_For example_, the following URN might be used to name the Internet standards document “RFC 2141” regardless of where it resides (it may even be copied in several places): 
urn:ietf:rfc:2141

---

## Transactions:

An HTTP transaction consists of a request command (sent from client to server), and a response result (sent from the server back to the client). This communication happens with formatted blocks of data called HTTP messages.

![[transactions.png]]

---

## Methods:

HTTP supports several different request commands, called HTTP methods. Every HTTP request message has a method. The method tells the server what action to perform (fetch a web page, run a gateway program, delete a file, etc.).


___Some common HTTP methods:___

| HTTP method | Description                                                          |
| ----------- | -------------------------------------------------------------------- |
| GET         | Send named resource from the server to the client.                   |
| PUT         | Store data from client into a named server resource.                 |
| DELETE      | Delete the named resource from a server.                             |
| POST        | Send client data into a server gateway application.                  |
| HEAD        | Send just the HTTP headers from the response for the named resource. |

---

## Status Codes:

Every HTTP response message comes back with a status code. The status code is a three-digit numeric code that tells the client if the request succeeded, or if other actions are required.


___Some common HTTP status codes:___

| HTTP status code | Description                                      |
| ---------------- | ------------------------------------------------ |
| 200              | OK. Document returned correctly.                 |
| 302              | Redirect. Go someplace else to get the resource. |
| 404              | Not Found. Can’t find this resource.             |

HTTP also sends an explanatory textual “_reason phrase_” with each numeric status code. The textual phrase is included only for descriptive purposes; the numeric code is used for all processing.

---

## Web Pages Can Consist of Multiple Objects:

An application often issues multiple HTTP transactions to accomplish a task. _For example_, a web browser issues a cascade of HTTP transactions to fetch and display a graphics-rich web page. The browser performs one transaction to fetch the HTML “_skeleton_” that describes the page layout, then issues additional HTTP transactions for each embedded image, graphics pane, Java applet, etc. These embedded resources might even reside on different servers. Thus, a _web page_ often is a collection of resources, not a single resource.

![[web_pages.png]]

---

## Messages:

HTTP messages are simple, line-oriented sequences of characters. Because they are plain text, not binary, they are easy for humans to read and write.

HTTP messages sent from web clients to web servers are called request messages. Messages from servers to clients are called response messages. There are no other kinds of HTTP messages. The formats of HTTP request and response messages are very similar.

![[messages.png]]

HTTP messages consist of three parts:
1. ___Start line___
	The first line of the message is the start line, indicating what to do for a request or what happened for a response.

2. ___Header fields___
	Zero or more header fields follow the start line. Each header field consists of a name and a value, separated by a colon (:) for easy parsing. The headers end with a blank line.

3. ___Body___
	After the blank line is an optional message body containing any kind of data. Request bodies carry data to the web server; response bodies carry data back to the client. Unlike the start lines and headers, which are textual and structured, the body can contain arbitrary binary data (e.g., images, videos, audio tracks, software applications). Of course, the body can also contain text.

![[messages_example.png]]

---

## TCP/IP:

HTTP is an application layer protocol. HTTP doesn’t worry about the nitty-gritty details of network communication; instead, it leaves the details of networking to TCP/IP, the popular reliable Internet transport protocol.

TCP provides:
- Error-free data transportation.
- In-order delivery (data will always arrive in the order in which it was sent).
- Unsegmented data stream (can dribble out data in any size at any time).

The Internet itself is based on TCP/IP, a popular layered set of packet-switched network protocols spoken by computers and network devices around the world. TCP/IP hides the peculiarities and foibles of individual networks and hardware, letting computers and networks of any type talk together reliably.

Once a TCP connection is established, messages exchanged between the client and server computers will never be lost, damaged, or received out of order.

In networking terms, the HTTP protocol is layered over TCP. HTTP uses TCP to transport its message data. Likewise, TCP is layered over IP.

![[internet_stack.png]]

---

## Connections, IP Addresses, and Port Numbers:

Before an HTTP client can send a message to a server, it needs to establish a TCP/IP connection between the client and server using _Internet protocol_ (IP) addresses and _port numbers._

Setting up a TCP connection is sort of like calling someone at a corporate office. First, you dial the company’s phone number. This gets you to the right organization. Then, you dial the specific extension of the person you’re trying to reach.

In TCP, you need the IP address of the server computer and the TCP port number associated with the specific software program running on the server.

This is all well and good, but how do you get the IP address and port number of the HTTP server in the first place? Why, the URL, of course! We mentioned before that URLs are the addresses for resources, so naturally enough they can provide us with the IP address for the machine that has the resource.

_Let’s take a look at a few URLs:_
http://207.200.83.29:80/index.html
http://www.netscape.com:80/index.html
http://www.netscape.com/index.html

The first URL has the machine’s IP address, “207.200.83.29”, and port number, “80”.

The second URL doesn’t have a numeric IP address; it has a textual domain name, or host-name ("www.netscape.com"). The host-name is just a human-friendly alias for an IP address. Host-names can easily be converted into IP addresses through a facility called the ___Domain Name Service___ (__DNS__), so we’re all set here, too.

The final URL has no port number. When the port number is missing from an HTTP URL, you can assume the default value of port __80__. With the IP address and port number, a client can easily communicate via TCP/IP.

![[connections_ip_addr_port_nums.png]]

_Here are the steps:_
1. The browser extracts the server’s host-name from the URL.
2. The browser converts the server’s host-name into the server’s IP address.
3. The browser extracts the port number (if any) from the URL.
4. The browser establishes a TCP connection with the web server.
5. The browser sends an HTTP request message to the server.
6. The server sends an HTTP response back to the browser.
7. The connection is closed, and the browser displays the document.

---

## A Real Example Using Telnet:

The ___Telnet___ utility connects your keyboard to a destination TCP port and connects the TCP port output back to your display screen. Telnet is commonly used for remote terminal sessions, but it can generally connect to any TCP server, including HTTP servers.

You can use the Telnet utility to talk directly to web servers. Telnet lets you open a TCP connection to a port on a machine and type characters directly into the port. The web server treats you as a web client, and any data sent back on the TCP connection is displayed onscreen.

Let’s use Telnet to interact with a real web server. We will use Telnet to fetch the document pointed to by the URL http://www.joes-hardware.com:80/tools.html. Let’s review what should happen:
- First, we need to look up the IP address of www.joes-hardware.com and open a TCP connection to port 80 on that machine. Telnet does this legwork for us.
- Once the TCP connection is open, we need to type in the HTTP request.
- When the request is complete (indicated by a blank line), the server should send back the content in an HTTP response and close the connection.

**_`Note: Telnet only works with HTTP, not HTTPS, because it doesn't support encryption. Since most websites now use HTTPS by default, Telnet can't be used to connect to them.`_**
Thus, we are going to create local http server to try a similar example. Here's a simple HTTP server with Java, you can copy it and paste in any IDE you like.
(**_Don't worry if you didn't understand that code, you don't have to learn how to create a web server now, we're going to learn it later_**).

~~~java
package main.java;  
  
import com.sun.net.httpserver.HttpServer;  
import com.sun.net.httpserver.HttpHandler;  
import com.sun.net.httpserver.HttpExchange;  
  
import java.io.IOException;  
import java.io.OutputStream;  
import java.net.InetSocketAddress;  
  
public class Main {  
    public static void main(String[] args) throws IOException{  
        SimpleHttpServer shs = new SimpleHttpServer();  
        shs.runHttpServer();  
    }  
}  
  
class SimpleHttpServer {  
    public void runHttpServer() throws IOException {  
        HttpServer server = HttpServer.create(new InetSocketAddress(8080), 0);  
  
        server.createContext("/content.html", new ContentPage());  
        server.start();  
    }  
  
    static class ContentPage implements HttpHandler {  
        @Override  
        public void handle(HttpExchange exchange) throws IOException {  
            String response = """  
        <!doctype html>        <html lang="en">            <head>                <meta charset="UTF-8">                <meta name="viewport"                      content="width=device-width, initial-scale=1.0">                <title>Simple Server</title>            </head>            <body>                <h1>Hello, sweetie!</h1>                <p>This is just a simple local HTTP server to mimic the example!</p>            </body>        </html>        """;  
            exchange.sendResponseHeaders(200, response.length());  
  
            OutputStream outputStream = exchange.getResponseBody();  
            outputStream.write(response.getBytes());  
            outputStream.close();  
        }  
    }  
}
~~~

After you run that HTTP server, you can try Telnet, but make sure to leave the program running, so it will be an active server.

~~~shell
telnet localhost 8080
Trying ::1...
Connected to localhost.
Escape character is '^]'.
GET /content.html HTTP/1.1
HOST: localhost

HTTP/1.1 200 OK
Date: Fri, 17 Oct 2025 17:43:40 GMT
Content-length: 358

<!doctype html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport"
              content="width=device-width, initial-scale=1.0">
        <title>Simple Server</title>
    </head>
    <body>
        <h1>Hello, sweetie!</h1>
        <p>This is just a simple local HTTP server to mimic the example!</p>
    </body>
</html>
Connection closed by foreign host.
~~~

- Telnet looks up the host-name and opens a connection to the _localhost_, which is listening on port 8080. The three lines after the command are output from Telnet, telling us it has established a connection.
- We then type in our basic request command, “_GET /content.html HTTP/1.1_”, and send a Host header providing the original host-name "_localhost_", followed by a blank line, asking the server to GET us the resource “_/content.html_” from the server "_localhost_". After that, the server responds with a response line, several response headers, a blank line, and finally the body of the HTML document.

---

## Architectural Components of the Web:

we’ve focused on how two web applications (web browsers and web servers) send messages back and forth to implement basic transactions. There are many other web applications that you interact with on the Internet. In this section, we’ll outline several other important applications, _including_:
- __Proxies__
	HTTP intermediaries that sit between clients and servers.
- __Caches__
	HTTP storehouses that keep copies of popular web pages close to clients.
- __Gateways__
	Special web servers that connect to other applications.
- __Tunnels__
	Special proxies that blindly forward HTTP communications.
- __Agents__
	Semi-intelligent web clients that make automated HTTP requests.


### Proxies:

___HTTP proxy servers___, important building blocks for web security, application integration, and performance optimization.

A proxy sits between a client and a server, receiving all of the client’s HTTP requests and relaying the requests to the server (perhaps after modifying the requests). These applications act as a proxy for the user, accessing the server on the user’s behalf.

Proxies are often used for security, acting as trusted intermediaries through which all web traffic flows. Proxies can also filter requests and responses; for example, to detect application viruses in corporate downloads or to filter adult content away from elementary-school students.

![[web_proxy.png]]


### Caches:

A ___web cache___ or ___caching proxy___ is a special type of HTTP proxy server that keeps copies of popular documents that pass through the proxy. The next client requesting the same document can be served from the cache’s personal copy. A client may be able to download a document much more quickly from a nearby cache than from a distant web server. HTTP defines many facilities to make caching more effective and to regulate the freshness and privacy of cached content.

![[web_cache.png]]


### Gateways:

___Gateways___ are special servers that act as intermediaries for other servers. They are often used to convert HTTP traffic to another protocol. A gateway always receives requests as if it was the origin server for the resource. The client may not be aware it is communicating with a gateway.

_For example_, an HTTP/FTP gateway receives requests for FTP URIs via HTTP requests but fetches the documents using the FTP protocol. The resulting document is packed into an HTTP message and sent to the client.

![[web_gateway.png]]


### Tunnels:

___Tunnels___ are HTTP applications that, after setup, blindly relay raw data between two connections. HTTP tunnels are often used to transport non-HTTP data over one or more HTTP connections, without looking at the data.

One popular use of HTTP tunnels is to carry encrypted _Secure Sockets Layer_ (SSL) traffic through an HTTP connection, allowing SSL traffic through corporate firewalls that permit only web traffic.

![[web_tunnel.png]]

An HTTP/SSL tunnel receives an HTTP request to establish an outgoing connection to a destination address and port, then proceeds to tunnel the encrypted SSL traffic over the HTTP channel so that it can be blindly relayed to the destination server.


### Agents:

___User agents___ (or just ___agents___) are client programs that make HTTP requests on the user’s behalf. Any application that issues web requests is an HTTP agent. So far, we’ve talked about only one kind of HTTP agent: web browsers. But there are many other kinds of user agents.

_For example_, there are machine-automated user agents that autonomously wander the Web, issuing HTTP transactions and fetching content, without human supervision. These automated agents often have colorful names, such as “_spiders_” or “_web robots_”.

![[user_agent.png]]

Spiders wander the Web to build useful archives of web content, such as a search engine’s database or a product catalog for a comparison-shopping robot.

---
---

> ___تم بحمد الله 3>___

---
---
