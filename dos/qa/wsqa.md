# dos
## Web Services
### QA
#### p1
#### p1
- What do you mean by Web Service?
  Web services, as the name suggests, is simply a software system that is specially designed to propagate communication between the client and server applications on WWW (World Wide Web). In simple words, it is the method of communication among two or more devices over a network. It allows multiple applications built on different programming languages to communicate with each other without any trouble. It uses the internet for direct application-to-application interaction, and also allows you to expose business logic using API.
- Web Services Interview Questions for Freshers
1. Explain different types of Web Services.
   There are basically two types of web services:


SOAP (Simple Object Access Protocol) Web Services: It is also referred to as transport-independent messaging protocol whose main purpose is to transfer a message, and is based on XML protocol.

RESTful (Representational State Transfer) Web Services: It is developed to fulfill the shortcomings of SOAP and to make the web services more effective.

2. What are the important features of Web services?
   Some of the important features of web services include:

Used to standardized XML messaging system.
Not tied to any one programming language or any operating system.
Discoverable via a simple find mechanism.
Available over the internet or private networks.
Supports loosely coupled connections between systems.
Can be synchronous or asynchronous.
Supports the transparent exchange of data to facilitate business integration.
Supports communication among different apps with HTML, XML, WSDL, SOAP, etc.
Supports RPC (Remote Procedure Calls).
3. What are the different components of Web Services?
   There are various components of web services as given below:

SOAP (Simple Object Access Protocol)
UDDI (Universal Description, Discovery, and Integration)
WSDL (Web Services Description Language)
RDF (Resource Description Framework)
XML (Extensible Markup Language)

4. Write the difference between API and Web services.
   API (Application Programming Interface): It acts as an interface between two devices so that they can communicate with each other without any user intervention. Some of its features include customizable, easy integration with GUI, time effective, language-independent, etc. All APIs are not web services.
   Web Service: It facilitates interaction between two devices over a network. They are widely used for exchanging data among systems or applications. Some of its features include loosely coupled, supports document exchange, interoperability, extensibility, etc. All Web services are APIs.

API	Web Service
It can be online or offline.	It must use a network.
They are lightweight architecture.	They require SOAP to send and receive network data therefore, are not lightweight architectures.
It can use any design style or protocol.	It can only use SOAP but sometimes UDDI, XML, RPC, and REST also.
It supports HTTP/HTTPS protocol and also supports XML and JSON.	It supports HTTP protocol and also supports XML.
It doesn’t require any network for its operation.	It requires a network for its operation.
They are open source and are used for XML.	They are not open source and are used to understand JSON (JavaScript Object Notation).
5. Name the tools that are used to test web services.
   There are various tools used to test web service as given below:

SoapUI
Poster
Postman
REST client
JMeter
6. What is WSDL?
   WSDL (Web Services Description Language), as the name suggests, is considered the standard format that is used to describe the availability of web services and how to access them. It is based on XML protocol for exchanging data in decentralized and distributed environments. It also describes the technical details or locates the user interface to the web service. WSDL document contains some important information as given below:

Method name and parameters  
Port types
Service endpoint
Header information, etc.

7. What is XML-RPC?
   XML-RPC (Remote procedure call) is considered the most basic and simplest XML-based protocol to exchange data among different devices on a network. It uses HTTP as a transport protocol for quickly and easily transferring the information or data between two devices. XML-RPC can also be used with different programming languages such as Perl, Java, Python, C, C++, PHP, etc.


8. What are the features of XML-RPC?
   There are various features of XML-RPC that includes:

Platform independent
Allows diverse applications to communicate
Considered as the easiest and simplest way to get started with web services
Uses XML to encode its calls and HTTP as the transport protocol
9. What do you mean by UDDI?
   UDDI (Universal Description, Discovery, and Integration) is a directory service used for describing, publishing, and finding web services. It is also used for creating business registries. It is based on a set of web standards including HTTP, XML, SOAP, WSDL, XML Schema. Its main goal is to streamline digital transactions and e-commerce among company systems.


10. What are the important features of UDDI?
    Some important features of UDDI include:

Platform independent
Uses WSDL for describing interfaces to web services
Can communicate through SOAP, Java RMI, and CORBA Protocol
The delineation between interface and implementation
Neutral in terms of protocols
11. Name the language that is commonly used by UDDI.
    The language commonly used by UDDI is WSDL (Web Service Description Language).

12. Explain web service Architecture.
    Every framework requires some type of architecture to ensure that the entire framework works perfectly as desired, the same goes for web services. Web service architecture is used to assist the developer with steps and procedures that are essential to complete the creation. Web service architecture includes three distinct roles i.e., service provider, service requester, and service registry. It also includes three different operations that include:

Publish (Publication of Service Descriptions): A service description needs to be published so that the service requestor can locate and have access to it. It can be published anywhere depending upon the requirements of the application.

Find (Finding of Services Descriptions): A service description is retrieved directly by a service requestor. The requestor consults the broker to locate a web service that is already published.

Bind (Invoking of Service based on Service Description): Every service needs to be invoked. To locate, contact, and invoke the service, the service requestor initiates the interaction with the service at runtime using details of binding in the service description.


13. What is a Web Service Provider?
    Web service generally creates web services and provides access to the client application who wants it. Its main purpose is to implement the service and make it available on the Internet so that client applications can use it whenever required. In simple words, it is a platform that creates and hosts web services.

14. What is a Web service Requestor?
    Web service requestor is the client application that requests for web service to use it. Its main purpose is to use an existing web service by opening a network connection and sending an XML request. In simple words, they are consumers of the web service.

15. What is a Web Service Registry?
    The web service registry is basically like a ‘phone book’ for web services. It allows client applications to be able to publish new services or can locate the already existing ones. Two widely-used registry standards are generally supported by application servers i.e., ebXML (Electronic Business using XML) and UDDI (Universal Description, Discovery, and Integration).

16. What are the different layers of the web service protocol stack?
    The implementation of web services generally depends on technologies that are often organized in a layered stack. Examining the web service protocol stack is considered as the second option for viewing the web service architecture. In simple words, it is the set of protocols that are used to explore and execute web services. Currently, the web service protocol stack has four layers as given below:


Service Transport: It is generally responsible to transport messages between applications. It basically defines technology standards for communication and allows messages or information to move across the network without any difficulty. It uses HTTP, SMTP, FTP, and DEEP protocols to transfer information.  
XML Messaging: It is generally responsible to encode messages into XML format so that one can understand these messages at either end. This layer generally includes XML-RPC and SOAP.  
Service Description: It is generally responsible to describe the public interface to a specific web service. WSDL is generally used to handle service descriptions.
Service Discovery: It is generally responsible to centralize service into a common registry and provides easy functionality for publishing or finding web services. UDDI is generally used to handle service discovery.

17. Explain the term Synchronicity.
    Synchronicity generally refers to the binding of the client to the function’s execution and it can be done in two ways i.e., synchronous and asynchronous. In Synchronous invocations, the client blocks and waits until the service complete its operation before continuing its work. In Asynchronous invocations, clients are allowed to invoke a service and execute other functions.

18. What are RESTful Web Services?
    REST (Representational State Transfer) is a stateless client-server architecture style used for developing applications that are accessible over the web. It is a type of web service whose main goal is to make web services more effective. It can be defined as the web service that uses HTTP methods for implementing the REST architecture. Unlike SOAP which is protocol-based, Restful services are architecturally based. It does not contain any contract or WSDL file.


19. What are the advantages of RESTful web service?
    There are several advantages of RESTful web services as given below:

Platform independent.
Simple and easy to implement and test.
Support different formats such as JSON, XML, HTML, etc.
Can be written in different programming languages and executed on any platform.
Lightweight, manageable, scalable, and reusable.
Faster and provide better performance.
Consume less bandwidth and resources.
A lot of automation framework is available
20. Which protocol is used by RESTful web services?
    The protocol used by RESTful web services is HTTP.

21. Explain the term statelessness with respect to RESTful web Services. Write its advantages.
    Statelessness is basically a condition or restriction where RESTful web services are not allowed to keep a client state on the server as per the REST architecture. Clients are responsible to pass their context to the server. To process the client’s request, the server then further stores this context.

Advantages:

No need to maintain previous interactions with clients.
Independent treatment of each method request.
Less complexity and simplified application design.
Example: Simple GET Request using NodeJS

We have the following sample data in users.json file.
Filename: users.json

{
"user1" : {
"name" : "gourav",
"password" : "password1",
"profession" : "officer",
"id": 1
},

"user2" : {
"name" : "nikhil",
"password" : "password2",
"profession" : "teacher",
"id": 2
}
}
Implement our RESTful API listUsers using the following code in a server.js file.
Filename: server.js

// Requiring module
var express = require('express');
var app = express();
var fs = require("fs");
// Sample GET API
app.get('/listUsers', function (req, res) {
fs.readFile( __dirname + "/" + "users.json", 'utf8', function (err, data) {
console.log( data );
res.end( data );
});
})
// Server setup
var server = app.listen(8081, function () {
var host = server.address().address
var port = server.address().port
console.log("Example app listening at http://%s:%s", host, port)
})
Now open a browser and go to http://127.0.0.1:8081/listUsers,  we will get the following response:

{
"user1" : {
"name" : "gourav",
"password" : "password1",
"profession" : "officer",
"id": 1
},

"user2" : {
"name" : "nikhil",
"password" : "password2",
"profession" : "teacher",
"id": 2
}
}
22. Name HTTP methods that can be used with RESTful web services.
    Some of the HTTP methods that can be used with RESTful web services include:

GET: Used to get and read a resource.
POST: Used to create a new resource.
PUT: Used to update existing resources.
DELETE: Used to delete the resource.
PATCH: Used to apply partial modifications to a resource.
23. What are the written status codes for REST API?
    REST API generally returns the following status codes in HTTP response:

200 OK
201 Created
202 Accepted
302 Found
400 Bad Request
401 Unauthorized
404 Not Found
405 Method Not Allowed
409 Conflict
500 Internal Server Error
24. What do you mean by SOAP? Write its advantages.
    SOAP (Simple Object Access Protocol) is an XML-based protocol that is used to access web services. It is simply used to interchange data or information between two devices or computers using request and response based on XML format over transport protocols like HTTP, SMTP, etc.


Advantages:

Language and Information independent.
Can be written in different programming languages or operating systems.
Provide data transport for web services.  
Can extend HTTP for XML messaging.
Defines and uses its own WS security.
Easy to debug and eliminate firewall issues.
25. What are the different elements of the SOAP Document or message?
    The SOAP message is basically an ordinary XML document consists of three parts as given below:

SOAP Envelope: It is a mandatory element that identifies XML documents as a SOAP message. It simply defines the start and the end of the message.

SOAP Header: It is an optional element that contains header information.

SOAP Body: It is a mandatory element that contains call and response information. It includes XML data consisting of the message that is being sent.


The following block depicts the general structure of SOAP XML request and response:

XML Request

<Envelope xmlns=?http://schemas.xmlsoap.org/soap/envelop/?>   
<Body>   
    <getCourseDetailRequest xmlns=?http://udemy.com/course?>   
       <id>course1</id>   
    <getCourseDetailRequest>   
</Body>   
</Envelope>  
XML Response 

<SOAP-ENV:Envelope xmlns:SOAP-ENV=?http://schemas.xmlsoap.org/soap/envelope/?>   
<SOAP-ENV:Header />          <!?empty header-->   
<SOAP-ENV:Body>             <!?body begin-->   
<ns2:getCourseDetailsResponse xmlns:ns2=?http://in28mi> <!--content of the response-->   
<ns2:course>   
<ns2:id>Course1</ns2:id>   
<ns2:name>Spring<ns2:name>   
<ns2:description>10 Steps</ns1:description>   
</ns2:course>   
</ns2:getCourseDetailResponse>   
</SOAP-ENV:Body>    <!?body end-->   
</SOAP-ENV:Envelope>
26. What do you mean by SOA?
    SOA (Service Oriented Architecture) is basically an architectural approach that is specially designed to support service orientation. It enabled services to communicate or interact across different platforms and languages to form applications. Applications in SOA are developed on the basis of services. It can be easily implemented using different protocols such as HTTP, JMS, HTTPS, RPC, RMI, etc.

27. What are the advantages of using SOA
    Some of its advantages include:

Easy to integrate.
Services are platform-independent.
Manage complexity so that integration becomes more manageable.
Services are easier to test and debug.
Easily available to any requester.
28. Name three primary security issues of Web Services?
    The three primary security issues of web services include:

Confidentiality
Authentication
Network Security
29. Name some components that are needed to be published while deploying a web service.
    Components that are needed to be published while deploying a web service includes:

Web Application Directory
Webservice.asmx File
Webservice.Disco File
Web.Config File
Bin Directory
Web Services Interview Questions for Experienced
30. Why is Web service important?
    Web services are very important as they provide standardized web protocols I.e., HTTP or HTTPS simply to interoperate, communicate, and exchange information in XML format via the internet. Some of its advantages include:

Allows devices to talk to each other and share data or services between themselves.
Makes the application platform and technology independent.
Uses standardized standard protocol for communication.  
User SOAP over HTTP protocol so that one can use their low-cost internet for implementing web services.
Allows business logic of different systems to be available over the web.
Can be used at the same time by many client applications.
31. Explain the term Distributed Technologies.
    Distributed technologies are in high demand nowadays because of the increasing ratio of distributed applications. It simply enables segmenting of application units and transferring these units to various computers on different networks.

32. What do you mean by DISCO?
    DISCO (Discovery), as the name suggests, is a Microsoft technology that is being used to discover web services. It is the process of locating and interrogating web service descriptions which is a preliminary step for having access to web services over the Internet.  The organization that provides web services generally provides a DISCO file on its server that includes the links of all the available web services so that it can be used within the local network.

33. Explain wsimport?
    Wsimport is basically a command-line tool that processes an existing WSDL file to generate all required web service artifacts for a web service client to access the published web services. It also supports a top-down approach for developing JAX-WS web services. In simple words, it generates Java classes from WSDL.

34. What is an Entrust Entitlement Service?
    EES (Entrust Entitlement Service), generally refers to a service that verifies entities that attempt to access a web service.

35. What do you mean by EIS and EPS?
    EIS (Entrust Identification Service): It is basically generated from Entrust security platform which allows or enables the corporates simply to handle and control the identities that are trusted to perform transactions for web service transactions.

EPS (Entrust Privacy Service): It deals with security and confidentiality simply by encrypting data. It is done to make sure that only concerned parties or authorized ones can have access to data.

36. What do you mean by Java Web services? Name the methods to create web services.
    Java web services is basically a type of web service that is being designed to develop and deploy basic web service on the Java platform. Java web service applications perform communication through WSDL and these applications can be accessed by different programming languages including .Net, PHP, etc. Two ways to write java web application code include SOAP and RESTful.


37. What do you mean by JAX-WS API? Write some implementations of JAX-WS API.
    JAX-WS (Java API for SOAP Web Services) is basically an essential part of the Java EE platform that is being used for developing or building SOAP web services and clients that communicate using XML. It enables developers to write message-oriented and RPC-oriented web services. There are basically two important implementations of JAX-WS:

RPC Style: It generates WSDL documents on the basis of the method name and its parameters. There are no type definitions present in the WSDL document.

Document Style: In this, one can transport XML messages as a part of SOAP requests unlike in RPC-style web service.

38. Name some important annotations of JAX-WS.
    Some important annotations of JAX-WS include:

@WebService
@WebMethod
@SOAPBinding
@WebResult
@WebServiceClient
39. What do you mean by JAX-RS API? Write some implementations of JAX-RS API.
    JAX-RS (Java API for RESTful web services) is basically an essential part of the Java EE platform that is being used for developing or building RESTful web services. There are basically two important implementations of JAX-RS API:

Jersey
RESTEasy
40. Name some important annotations of JAX-RS API.
    Some important annotations of the JAX-RS API include:

@Path: It is specially used to specify the relative path of resource class and methods. This annotation can be used on any class or method in code. It binds the URI pattern to a Java method.
@GET, @PUT, @POST, @DELETE, @HEAD: It is specially used to specify HTTP request type for a method. These annotations can be specified on the JAX-RS method.
@Produces: This annotation is specially used to specify HTTP responses generated by web services.
@Consumes: This annotation is specially used to specify HTTP Requests.  
@PathParam: It is specially used to specify parameters to path value by parsing.
41. Name two Microsoft solutions for distributed applications.
    The two Microsoft solutions for distributed applications include:

.NET Web Services
.NET Remoting
42. Is there any need for a special application to have access to the Web service?
    No, there is no need for a special application to have access to the Web service. One can access web applications from any of the applications that support XML-based object requests and responses.

43. What do you mean by sun-jaxws.xml file?
    Sun-jaxws.xml file is simply used to provide endpoint details when JAX-WS web services are deployed as a standard WAR archive on a servlet container like Tomcat. It is also available in the WEB-INF directory.

Example:

<?xml version="1.0" encoding="UTF-8"?> 
<endpoints xmlns="http://java.sun.com/xml/ns/jax-ws/ri/runtime" version="2.0"> 
 <endpoint 
    name="HelloWorldWS" 
    implementation="org.arpit.javapostsforlearning.webservice.HelloWorldImpl" 
    url-pattern="/HelloWorldWS"/> 
</endpoints> 
44. What is BEEP?
BEEP (Blocks Extensible Exchange Protocol) is basically an IETF (Internet Engineering Task Force) framework that is generally used to develop network application protocols. One can create these new protocols for different applications such as instant messaging, network management, file transfer, content syndication, etc. It is directly layered over TCP. BEEP has various in-build features such as authentication, security, initial handshake protocol, error handling, etc. 

45. Give an example of working for a Web Service Provider.
    using System;   
    using System.Web.Services;   
    using System.Xml.Serialization;   
    [WebService(Namespace="http://localhost/MyWebServices/")]   
    public class FirstService : WebService  
    {   
    [WebMethod]   
    public int Add(int a, int b)  
    {   
    return a + b;   
    }   
    [WebMethod]   
    public String SayHello()  
    {   
    return "Hello World";   
    }   
    }
46. What is the importance of URI in REST based web services?
    In REST-based web services, URI (Uniform Resource Locator) is generally used to locate resources on the server that is hosting the web service. Each resource in service will have at least one URI that is used to identify it. Web services clients generally use URI to access the resource. Its format is given below:

<protocol>://<service-name>/<ResourceType>/<ResourceID>


47. What's the importance of security in web services?
    Security is considered a very important feature in any web application. It is essential in web services so that we can make confidential or sensitive information and transactions more reliable. In web services, the security is attained through SSL (Service Socket Layer) that helps in developing EST (Entrust Secure Transaction) platform.

48. What’s the difference between Web services and CORBA or DCOM?
    Web service	CORBA and DCOM
    Web services basically transfer messages to applications or receive messages from applications using the HTTP protocol. To encode data, a web service uses XML. 	They basically transfer messages to applications or receive messages from applications using non-standard protocols like RPC, IIOP (Inter Internet Object Protocol), etc.
    WSDL is used to define web services.	CORBA Interface Description Language is used to define CORBA components and Microsoft Interface Definition Language is used to define DCOM components.
    UDDI is used to discover web services.	CORBA registry is used to define CORBA components and DCOM registry is used to define DCOM components.
    They are firewalls friendly.	CORBA uses IIOP protocol i.e., non-internet friendly.
49. What are .NET Web services and .NET Remoting? Write the difference between them.
    .NET Remoting: It is a method that enables objects to communicate or interact with each other across application domains, processes, and machine boundaries, whether application components are present in one computer or different computers across the entire world.

.NET Web service: It is a method that enables cross-platform integration by using XML, HTTP, and SOAP for communication among two devices over WWW. It simply shares business logic, processes, and data through programmatic interfaces across a network.

Both of them are powerful technologies that provide suitable frameworks and thus support the development of distributed technologies and application integration. There is some difference between these two technologies as given below.

Web Services	.NET Remoting
It uses HTTP protocol. 	It uses TCP/HTTP/SMTP protocol.
Its performance is slow as compared to .NET Remoting. 	It provides faster communication and performance when one uses the TCP channel and the binary formatter.
These services are hosted using IIS and therefore, are more reliable. 	It is less reliable as compared to .NET Web services.
It supports the XML Schema type system and provides a very simple programming model along with broad cross-platform reach.	It supports a runtime type system and provides a complex programming model along with very limited reach.
50. How to implement web services in .NET?
    HTTP Handles are generally used to implement web services in .NET because HTTP handles interrupt requests to .asmx files.

51. What is the importance of using @XmlRootElement?
    The main purpose of @XmlRootElement is to transform or convert Java objects to XML and vice versa. It is generally the base common annotation used for JAXB API. It uniquely associates a root element with a class.

52. Explain the term JAXP.
    JAXP (Java API for XML Processing) is basically a Java API that allows parsing, transform, validate, and queries XML files with DOM (Document Object Model), SAX (Simple API for XML), or StAX (Streaming API for XML) Parsers/Parsing interfaces. It is used for processing XML data using applications that are written in Java programming language.

53. What is JAXB? Name three different packages in JAXB binding framework.
    JAXB (Java Architecture for XML Binding) is basically a Java standard that is used to define how Java objects get converted into XML and vice-versa. Using Java facilitates the reading and writing of XML. It makes it easier to access XML documents from applications that are written in the Java programming language. There are three different packages in JAXB binding framework that includes:

xml.bind
xml.bind.util
xml.bind.helper

54. Name the web service method that is read-only, and is idempotent?
    The web service method that is read-only and safe is the GET method, and the web service methods that are idempotent are PUT and DELETE operations. Idempotent refers to the operations whose results will always be the same even if these operations are invoked so many times.

55. Explain Spring Web Service.
    Spring WS (Web Service) is basically a product of the spring community whose main focus is to develop document-driven web services. It only aims to facilitate contract-first SOAP service development. It allows the development of web services that are flexible.

56. Spring-WS support contract last development approach. Yes, or no?
    No, Spring-WS does not support the contract's last development approach. It only supports the contract-first development approach.

Conclusion
57. Conclusion
    Web services are considered as one of the key elements of programmable Web that allows individuals to communicate and share relevant information on two applications over the same network. It has become an essential and critical element of development for web developers. These services are effectively used to participate in and set up B2B transactions. The above given are the most important interview questions regarding Web services. Sharpen your knowledge before you face the interviewer.

Recommended Resources:

Web API Interview

REST API Interview



### references
#### links
- <https://www.interviewbit.com/web-services-interview-questions/>