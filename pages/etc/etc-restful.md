---
title: REST API
sidebar: mydoc_sidebar
permalink: etc_restful.html
folder: etc
---

### 1. Anatomy of REST 
>- **Resource - URI**
>- **Verb - HTTP Method**
>- **Representations**

### 2. Constraints to be RESTful

1. **Uniform Interface**
   - Decouple the client from the implemenation of the REST service
2. **Stateless**
   - Do not store state informaion like session and cookie
3. **Cacheable**
    - Possible to implement caching like Last-Modified Tag or E-Tag in HTTP protocol
4. **Self-descriptiveness**
5. **Client - Server seperation**
6. **Layered System**
    - Between the client and server, there can be middle layers like a security layer, a caching layer, a load-balancing layer, proxy, gateway or other functionality. 

### 3. RESTful Design Guide

> _First, **URI** should represent the **Resource**_.  
> _Second, **Operaion** of the Resource should be represented with **HTTP Method (GET, POST, PUT, DELETE)**_  

#### 1. URI represents the Resource (Use Noun for the Resource)
    (✕) :: GET /members/delete/1
    (○) :: DELETE /members/1

    (✕) :: GET /members/show/1
    (○) :: GET /members/1 

    (✕) :: GET /members/insert/2
    (○) :: POST /members/2  
  
#### 2. How to represent the relation between the Resources  
    /resouce/resource id/other resource  
    ex) GET /users/:userid/devices (has relation)  
    ex) GET /users/:userid/likes/devices (exceptionally possible when detailed representaion is required)   
  
#### 3. Collection and Document which represent the Resource  
    Document is an object and Collection is the collection of objects.  
    Collection and document are all Resource and represented in URI.  
    Collection should be plural!!!  
    ex) **http://restapi.example.com/sports/soccer/players/13**
    

### 4. HTTP Response Status Code

| Status code | Responses | Information responses|
| :------ |:--- | :--- |
| 200 | OK | The request has succeeded |
| 201 | Created | The request has succeeded and a new resource has been created as a result |
| 400 | Bad Request | The server could not understand the request due to invalid syntax |
| 401 | Unauthorized | the client must authenticate itself to get the requested response |
| 404 | Not Found | The server can not find the requested resource |
| 405 | Method Not Allowed | The request method is known by the server but has been disabled and cannot be used |
| 301 | Moved Permanently | The URL of the requested resource has been changed permanently. The new URL is given in the response |
| 500 | Internal Server Error | The server has encountered a situation it doesn't know how to handle |
