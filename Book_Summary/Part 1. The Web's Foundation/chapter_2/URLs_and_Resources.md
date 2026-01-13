
Uniform resource locators (URLs) are the standardized names for the Internet’s resources. URLs point to pieces of electronic information, telling you where they are located and how to interact with them.


---
---


## Navigating the Internet’s Resources

URLs are the resource locations that your browser needs to find information.

URLs actually are a subset of a more general class of resource identifier called a uniform resource identifier, or URI. URIs are a general concept comprised of two main subsets, URLs and URNs. URLs identify resources by describing where resources are located, whereas URNs identify resources by name, regardless of where they currently reside.

HTTP applications deal only with the URL subset of URIs.

_Say you want to fetch the URL_ "`http://www.joes-hardware.com/seasonal/index-fall.html`":
- The first part of the URL (_http_) is the URL ___scheme___. The scheme tells a web client how to access the resource. In this case, the URL says to use the HTTP protocol.
- The second part of the URL (`www.joes-hardware.com`) is the ___server location___. This tells the web client where the resource is hosted.
- The third part of the URL (_/seasonal/index-fall.html_) is the ___resource path___. The path tells what particular local resource on the server is being requested.

![[url_parts.png]]

URLs can direct you to resources available through protocols other than HTTP.


---
---


## URL Syntax

URLs provide a means of locating any resource on the Internet, but these resources can be accessed by different schemes (e.g., _HTTP_, _FTP_, _SMTP_), and URL syntax varies from scheme to scheme.

Most URL schemes base their URL syntax on this nine-part general format:
`<scheme>://<user>:<password>@<host>:<port>/<path>;<params>?<query>#<frag>`.

Almost no URLs contain all these components. The three most important parts of a URL are the ___scheme___, the ___host___, and the ___path___.


_General URL components:_

| Component | Description                                                                                                                                                                                                                                                                         | Default value     |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- |
| scheme    | Which protocol to use when accessing a server to get a resource.                                                                                                                                                                                                                    | None              |
| user      | The username some schemes require to access a resource.                                                                                                                                                                                                                             | anonymous         |
| password  | The password that may be included after the username, separated by a colon (:).                                                                                                                                                                                                     | `<Email address>` |
| host      | The host-name or dotted IP address of the server hosting the resource.                                                                                                                                                                                                              | None              |
| port      | The port number on which the server hosting the resource is listening. Many schemes have default port numbers (the default port number for HTTP is 80).                                                                                                                             | Scheme-specific   |
| path      | The local name for the resource on the server, separated from the previous URL components by a slash (/). The syntax of the path component is server- and scheme-specific.                                                                                                          | None              |
| params    | Used by some schemes to specify input parameters. Params are name/value pairs. A URL can contain multiple params fields, separated from themselves and the rest of the path by semicolons (;).                                                                                      | None              |
| query     | Used by some schemes to pass parameters to active applications (such as databases, bulletin boards, search engines, and other Internet gateways). There is no common format for the contents of the query component. It is separated from the rest of the URL by the “?” character. | None              |
| frag      | A name for a piece or part of the resource. The frag field is not passed to the server when referencing the object; it is used internally by the client. It is separated from the rest of the URL by the “#” character.                                                             | None              |

---

### Schemes: What Protocol to Use:

The ___scheme___ is the main identifier of how to access a given resource; it tells the application interpreting the URL what protocol it needs to speak.

The scheme component must start with an alphabetic character, and it is separated from the rest of the URL by the first “:” character. Scheme names are case-insensitive, so the URLs (`http://www.joes-hardware.com`) and (`HTTP://www.joeshardware.com`) are equivalent.

---

### Hosts and Ports:

The ___host___ component identifies the host machine on the Internet that has access to the resource. The name can be provided as a host-name, as above (`www.joes-hardware.com`) or as an IP address.
_For example_, the following two URLs point to the same resource:
- `http://www.joes-hardware.com:80/index.html`
- `http://161.58.228.45:80/index.html`

The ___port___ component identifies the network port on which the server is listening. For HTTP, which uses the underlying TCP protocol, the default port is 80.

---

### Usernames and Passwords:

Many servers require a ___username___ and ___password___ before you can access data through them. FTP servers are a common example of this.

_Here are a few examples:_
- `ftp://ftp.prep.ai.mit.edu/pub/gnu` -> No _user_ or _password_ component, just our standard scheme, host, and path. If an application is using a URL scheme that requires a username and password, such as FTP, it generally will insert a default username and password if they aren’t supplied. _For example_, it will insert “anonymous” for your username and send a default password (Internet Explorer sends “IEUser”, while Netscape Navigator sends “mozilla”).
- `ftp://anonymous@ftp.prep.ai.mit.edu/pub/gnu` -> The username being specified as “anonymous”. This username, combined with the host component, looks just like an email address. The “@” character separates the user and password components from the rest of the URL.
- `ftp://anonymous:my_passwd@ftp.prep.ai.mit.edu/pub/gnu` -> both a username (“anonymous”) and password (“my_passwd”) are specified, separated by the “:” character.
- `http://joe:joespasswd@www.joes-hardware.com/sales_info.txt`

---

### Paths:

The ___path___ component of the URL specifies where on the server machine the resource lives. The path often resembles a hierarchical file-system path. _For example:_
	`http://www.joes-hardware.com:80/seasonal/index-fall.html`

---

### Parameters:

For many schemes, a simple host and path to the object just aren’t enough. Many protocols require more information to work.

Applications interpreting URLs need these protocol parameters to access the resource. Otherwise, the server on the other side might not service the request or, worse yet, might service it wrong. For example, take a protocol like FTP, which has two modes of transfer, binary and text. You wouldn’t want your binary image transferred in text mode, because the binary image could be scrambled.

To give applications the input parameters they need in order to talk to the server correctly, URLs have a ___params___ component. This component is just a list of "name/value" pairs in the URL, separated from the rest of the URL (and from each other) by “;” characters. They provide applications with any additional information that they need to access the resource. _For example:_ 
	`ftp://prep.ai.mit.edu/pub/gnu;type=d`

The path component for HTTP URLs can be broken into path segments. Each segment can have its own params. _For example:_
	`http://www.joes-hardware.com/hammers;sale=false/index.html;graphics=true` -> There are two path segments, hammers and index.html. The hammers path segment has the param sale, and its value is false. The index.html segment has the param graphics, and its value is true.

---

### Query Strings:

Some resources, such as database services, can be asked questions or queries to narrow down the type of resource being requested.

The following URL might be used to query a web database gateway to see if item number 12731 is available: 
	`http://www.joes-hardware.com/inventory-check.cgi?item=12731`

![[query_strings.png]]

---

### Fragments:

Some resource types, such as HTML, can be divided further than just the resource level. For example, for a single, large text document with sections in it, the URL for the resource would point to the entire text document, but ideally you could specify the sections within the resource.

URLs support a ___frag___ component to identify pieces within a resource. _For example_, a URL could point to a particular image or section within an HTML document.

A fragment dangles off the right-hand side of a URL, preceded by a # character. _For example_:
	`http://www.joes-hardware.com/tools.html#drills` -> The fragment drills references a portion of the /tools.html web page located on the Joe’s Hardware web server. The portion is named “drills”.

Because HTTP servers generally deal only with entire objects, not with fragments of objects, clients don’t pass fragments along to servers. After your browser gets the entire resource from the server, it then uses the fragment to display the part of the resource in which you are interested.

![[fragment.png]]


---
---


## URL Shortcuts

### Relative URLs:

URLs have two types: ___absolute___ and ___relative___.
- _Absolute_ URL -> You have all the information you need to access a resource.
- _Relative_ URLs -> Are incomplete. To get all the information needed to access a resource from a relative URL, you must interpret it relative to another URL, called its base.

_Example of relative URL in HTML:_ #Relative_URL_in_HTML 
~~~html
<html>
	<head>
		<title>Joe's Tools</title>
	</head>
	<body>
		<h1>Tools Page</h1>
		<h2>Hammers</h2>
		
		<p>Joe's Hardware Online has the largest selection of <a href="./hammers.html">hammers</a> on earth.</p>
		
	</body>
</html>
~~~

Our base URL is: `http://www.joes-hardware.com/tools.html`.

![[base_url.png]]


Relative URLs are only fragments or pieces of URLs. 

It is also worth noting that relative URLs provide a convenient way to keep a set of resources (such as HTML pages) portable. If you use relative URLs, you can move a set of documents around and still have their links work, because they will be interpreted relative to the new base. This allows for things like mirroring content on other servers.

---

### Base URLs:

The first step in the conversion process is to find a base URL. It can come from a few places:

- Explicitly provided in the resource:
	Some resources explicitly specify the base URL. An HTML document, for example, may include a HTML tag defining the base URL by which to convert all relative URLs in that HTML document. 
- Base URL of the encapsulating resource:
	If a relative URL is found in a resource that does not explicitly specify a base URL, as in Example above #Relative_URL_in_HTML , it can use the URL of the resource in which it is embedded as a base.
- No base URL:
	In some instances, there is no base URL. This often means that you have an absolute URL; however, sometimes you may just have an incomplete or broken URL.

---

### Resolving relative references:

The next step in converting a relative URL into an absolute one is to break up both the relative and base URLs into their component pieces. In effect, you are just parsing the URL, but this is often called decomposing the URL, because you are breaking it up into its components. Once you have broken the base and relative URLs into their components, you can then apply this algorithm.

![[decomposing_algorithm.png]]

---

### Expandomatic URLs:

These “expandomatic” features come in two flavors:
- Hostname expansion:
	In hostname expansion, the browser can often expand the hostname you type in into the full hostname without your help, just by using some simple heuristics. For example if you type “yahoo” in the address box, your browser can automatically insert “www.” and “.com” onto the hostname, creating “www.yahoo.com”. Some browsers will try this if they are unable to find a site that matches “yahoo”, trying a few expansions before giving up. Browsers apply these simple tricks to save you some time and frustration.
- History expansion:
	Another technique that browsers use to save you time typing URLs is to store a history of the URLs that you have visited in the past. As you type in the URL, they can offer you completed choices to select from by matching what you type to the prefixes of the URLs in your history. So, if you were typing in the start of a URL that you had visited previously, such as `http://www.joes-`, your browser could suggest `http://www.joes-hardware.com`. You could then select that instead of typing out the complete URL.


---
---


## Shady Characters

URLs were designed to be portable. They were also designed to uniformly name all the resources on the Internet, which means that they will be transmitted through various protocols. Because all of these protocols have different mechanisms for transmitting their data, it was important for URLs to be designed so that they could be transmitted safely through any Internet protocol. 

Safe transmission means that URLs can be transmitted without the risk of losing information. Some protocols, such as the Simple Mail Transfer Protocol (SMTP) for electronic mail, use transmission methods that can strip off certain characters. To get around this, URLs are permitted to contain only characters from a relatively small, universally safe alphabet. 

In addition to wanting URLs to be transportable by all Internet protocols, designers wanted them to be readable by people. So invisible, non-printing characters also are prohibited in URLs, even though these characters may pass through mailers and otherwise be portable.

To complicate matters further, URLs also need to be complete. URL designers realized there would be times when people would want URLs to contain binary data or characters outside of the universally safe alphabet. So, an ___escape mechanism___ was added, allowing unsafe characters to be encoded into safe characters for transport.

---

### The URL Character Set:

Some URLs may need to contain arbitrary binary data. Recognizing the need for completeness, the URL designers have incorporated escape sequences. ___Escape sequences___ allow the encoding of arbitrary character values or data using a restricted subset of the US-ASCII character set, yielding portability and completeness.

---

### Encoding Mechanisms:

The encoding simply represents the unsafe character by an ___escape___ notation, consisting of a percent sign (%) followed by two hexadecimal digits that represent the ASCII code of the character.


| Character | ASCII code | Example URL                                            |
| --------- | ---------- | ------------------------------------------------------ |
| ~         | 126 (0x7E) | `http://www.joes-hardware.com/%7Ejoe`                  |
| SPACE     | 32 (0x20)  | `http://www.joes-hardware.com/more%20tools.html`       |
| %         | 37 (0x25)  | `http://www.joes-hardware.com/100%25satisfaction.html` |

---

### Character Restrictions:

Several characters have been reserved to have special meaning inside of a URL. Others are not in the defined US-ASCII printable set. And still others are known to confuse some Internet gateways and protocols, so their use is discouraged.


| Character            | Reservation/Restriction                                                                                                                                                                       |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `%`                  | Reserved as escape token for encoded characters.                                                                                                                                              |
| `/`                  | Reserved for delimiting splitting up path segments in the path component.                                                                                                                     |
| `.`                  | Reserved in the path component.                                                                                                                                                               |
| `..`                 | Reserved in the path component.                                                                                                                                                               |
| `#`                  | Reserved as the fragment delimiter.                                                                                                                                                           |
| `?`                  | Reserved as the query-string delimiter.                                                                                                                                                       |
| `;`                  | Reserved as the params delimiter.                                                                                                                                                             |
| `:`                  | Reserved to delimit the scheme, user/password, and host/port components.                                                                                                                      |
| `$ , +`              | Reserved.                                                                                                                                                                                     |
| `@ & =`              | Reserved because they have special meaning in the context of some schemes.                                                                                                                    |
| `{ } \| \ ^ ~ [ ] ‘` | Restricted because of unsafe handling by various transport agents, such as gateways.                                                                                                          |
| `< > "`              | Unsafe; should be encoded because these characters often have meaning outside the scope of the URL, such as delimiting the URL itself in a document (e.g., “`http://www.joes-hardware.com`”). |
| 0x00–0x1F, 0x7F      | Restricted; characters within these hex ranges fall within the nonprintable section of the US-ASCII character set.                                                                            |
| > 0x7F               | Restricted; characters whose hex values fall within this range do not fall within the 7-bit range of the US-ASCII character set.                                                              |

Applications need to walk a fine line. It is best for client applications to convert any unsafe or restricted characters before sending any URL to any other application.
Once all the unsafe characters have been encoded, the URL is in a canonical form that can be shared between applications; there is no need to worry about the other application getting confused by any of the characters’ special meanings.

The original application that gets the URL from the user is best fit to determine which characters need to be encoded. Because each component of the URL may have its own safe/unsafe characters, and which characters are safe/unsafe is scheme-dependent, only the application receiving the URL from the user really is in a position to determine what needs to be encoded.


---
---


## A Sea of Schemes

More information about MIME: [[Appendixes]] -> #URI_Schemes  


---
---


## The Future

URLs are a powerful tool. Their design allows them to name all existing objects and easily encompass new formats. They provide a uniform naming mechanism that can be shared between Internet protocols.

However, they are not perfect. URLs are really addresses, not true names. This means that a URL tells you where something is located, for the moment. It provides you with the name of a specific server on a specific port, where you can find the resource. The downfall of this scheme is that if the resource is moved, the URL is no longer valid. And at that point, it provides no way to locate the object.

What would be ideal is if you had the real name of an object, which you could use to look up that object regardless of its location. As with a person, given the name of the resource and a few other facts, you could track down that resource, regardless of where it moved.

The Internet Engineering Task Force (IETF) has been working on a new standard, ___uniform resource names___ (URNs), for some time now, to address just this issue. URNs provide a stable name for an object, regardless of where that object moves (either inside a web server or across web servers).

___Persistent uniform resource locators___ (PURLs) are an example of how URN functionality can be achieved using URLs. The concept is to introduce another level of indirection in looking up a resource, using an intermediary resource locator server that catalogues and tracks the actual URL of a resource. A client can request a persistent URL from the locator, which can then respond with a resource that redirects the client to the actual and current URL for the resource.

![[PURLs.png]]

For more information on PURLs, visit http://purl.oclc.org.


---
---


## Done.
---
---

> ___تم بحمد الله 3>___

---
---
