---
title: Webservice
sidebar: mydoc_sidebar
permalink: etc_webservice.html
folder: etc
---

### 1. What is SOAP?

   SOAP stands for Simple Object Access Protocol. It’s a messaging protocol for interchanging data in a decentralized and distributed environment. SOAP can work with any application layer protocol, such as HTTP, SMTP, TCP, or UDP. It returns data to the receiver in XML format. Security, authorization, and error-handling are built into the protocol and, unlike REST, it doesn’t assume direct point-to-point communication. Therefore it performs well in a distributed enterprise environment. SOAP follows a formal and standardized approach that specifies how to encode XML files returned by the API. A SOAP message is, in fact, an ordinary XML file that consists of the following parts:

   - Envelope (required) – This is the starting and ending tags of the message.
   - Header (optional) – It contains the optional attributes of the message. It allows you to extend a SOAP message in a modular and decentralized way.
   - Body (required) – It contains the XML data that the server transmits to the receiver.
   - Fault (optional) – It carries information about errors occurring during processing the message.

### 2. What's the main reason to use SOAP?

   SOAP will likely continue to be used for enterprise-level web services that require high security and complex transactions. APIs for financial services, payment gateways, CRM software, identity management, and telecommunication services are commonly used examples of SOAP.

   Besides, SOAP can be an excellent solution in situations where you can’t use REST. Although these days, most web service providers want to exchange stateless requests and responses, in some cases, you may need to process stateful operations. This happens in scenarios where you have to make a chain of operations act as one transaction—for instance, in the case of bank transfers.

### 3. What is REST?

   REST stands for Representational State Transfer. It’s an architectural style that defines a set of recommendations for designing loosely coupled applications that use the HTTP protocol for data transmission. 
   nstead, the REST guidelines allow developers to implement the details according to their own needs. Web services built following the REST architectural style are called RESTful web services.

   1. Uniform interface – Requests from different clients should look the same, for example, the same resource shouldn’t have more than one URI.
   2. Client-server separation – The client and the server should act independently. They should interact with each other only through requests and responses.
   3. Statelessness – There shouldn’t be any server-side sessions. Each request should contain all the information the server needs to know.
   4. Cacheable resources – Server responses should contain information about whether the data they send is cacheable or not. Cacheable resources should arrive with a version number so that the client can avoid requesting the same data more than once.
   5. Layered system – There might be several layers of servers between the client and the server that returns the response. This shouldn’t affect either the request or the response.


### 4. The main difference between SOAP and REST

   SOAP and REST both allow you to create your own API. API stands for Application Programming Interface. It makes it possible to transfer data from an application to other applications. An API receives requests and sends back responses through internet protocols such as HTTP, SMTP, and others.
   SOAP is a standardized protocol that sends messages using other protocols such as HTTP and SMTP. 
   As opposed to SOAP, REST is not a protocol but an architectural style. The REST architecture lays down a set of guidelines you need to follow if you want to provide a RESTful web service, for example, stateless existence and the use of HTTP status codes.

   As SOAP is an official protocol, it comes with strict rules and advanced security features such as built-in ACID compliance and authorization. Higher complexity, it requires more bandwidth and resources which can lead to slower page load times.

   REST was created to address the problems of SOAP. Therefore it has a more flexible architecture. It consists of only loose guidelines and lets developers implement the recommendations in their own way. It allows different messaging formats, such as HTML, JSON, XML, and plain text, while SOAP only allows XML. REST is also a more lightweight architecture, so RESTful web services have a better performance. Because of that, it has become incredibly popular in the mobile era where even a few seconds matter a lot (both in page load time and revenue).

### 5. SOAP vs REST comparison table

|  | SOAP | REST|
| :------ |:--- | :--- |
| Meaning | Simple Object Access Protocol | Representational State Transfer |
| Design | Standardized protocol with pre-defined rules to follow | Achitectural style with loose guidelines and recommendations. |
| Approach | Function-driven (data available as services, e.g.: “getUser”) | Data-driven (data available as resources, e.g. “user”) |
| Statefulness | Stateless by default, but it’s possible to make a SOAP API stateful. | Stateless (no server-side sessions) |
| Caching | API calls cannot be cached. | API calls can be cached. |
| Performance | Requires more bandwidth and computing power | 	Plain text, HTML, XML, JSON, YAML, and others |
| Message format | Only XML | Requires fewer resources |
| Transfer protocol(s) | HTTP, SMTP, UDP, and others | 	Only HTTP |
| Recommended for | Enterprise apps, high-security apps, distributed environment, financial services, payment gateways, telecommunication services. | Public APIs for web services, mobile services, social networks |
| Advantages | EHigh security, standardized, extensibility | Scalability, better performance, browser-friendliness, flexibility |
| Disadvantages | Poorer performance, more complexity, less flexibility | Less security, not suitable for distributed environments. |
