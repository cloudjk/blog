---
title: Interview Questions
sidebar: mydoc_sidebar
permalink: node_interview_questions.html
folder: node
---

### 1. What is Node.js? What is it used for ?

   Node.js is a run-time Javascript environment built on top of Chrome's V8 engine.
   It is a single-threaded non-blocking asynchronous concurrent language. It is lightweight and efficient.
   cannot take advantage of multi core because it is a single-threaded. Cluseter is released in beta version recently for multi thread handling.

   Node.js can be used to build different type of applications such as web application,
   real-time chat applications, REST API server etc. However it is mainly used to build 
   network programs like web servers.

### 2. What is npm?

   the largest ecosystem of open-source libraries in the world.

### 4. What is Event loop in Node.js?

  ![Event Loop diagram](/assets/img/posts/eventloop.png)

### 5. Difference between dependencies and devDependencies

| Explanation | Command | Shortchut| dependencies|
| :------ |:--- | :--- | :--- | :--- |
| Install a pkg locally | npm install pkg | npm i pkg| ✕ |
| Install multiple pkgs locally | npm install pkg1 pkg2 ... | npm i pkg1 pkg2 ... | ✕ |
| Install pkg and save as dependency | npm install - -save pkg | npm i -S pkg | dependencies |
| Install multiple pkgs and save as dependency | npm install - -save pkg1 pkg2 ... | npm i -S pkg1 pkg2 ... | dependencies |
| Install pkg and save as devDependency | npm install - -save-dev pkg | npm i -D pkg | devDependencies |
| Install multiple pkgs and save as devDependency | npm install - -save-dev pkg1 pkg2 ... | npm i -D pkg1 pkg2 ... | devDependencies |
| Install global package | npm install -g pkg | npm i -g pkg| ✕ |
| Install dependencies, devDependencies | npm install | npm i | ALL |
| Install just dependencies | npm install - -only=prod[uction] | npm i - -only=prod[uction] | dependencies |
| Install just devDependencies | npm install - -only=dev[elopment] | npm i - -only=dev[elopment] | devDependencies |

### 6. What is REPL in Node.js ?
   REPL means Read-Eval-Print-Loop. It is a propt that comes with Node.js.
   We can quickly test our Javascript code in the REPL environment.

### 7. What is the purpose of module.exports ?

   A module encapsulates related code into a single unit of code. 
   This exposes functions to the outer world. We can import them in another file using require or import (typescript)

### 8. What is require in Node.js ? How will you load external files and libraries in Node.js ?

   require function is used to load external files and moduels that exist in separate files. The basic functionality of require
   is that it reads a JavaScript files, execute the file and then return the exports object. For example, consider the below
   code exist in example.js:

   ![export 1](/assets/img/posts/export.png)

   In another file, we can load this function with **require**.
   ![export 2](/assets/img/posts/require.png)

### 9. What is the difference between Asynchronous and Non-blocking ?

   Asynchronous literally means not synchronous. We are making HTTP requests which are asynchronous, means we are **not waiting**
   for the server response. We continue with other block and repond to the server response when we received.

   There is no difference in what they refer to. To be technical you could way they differ in emphasis. Non blocking refers to
   **control flow**(it doesn't block). Asynchronous refers to **when** they event/data is handled(not synchronously).

### 8. How will you debug an application ?

   Node.js includes a debugging utility called debugger. To enable it start the Node.js with 
   the debug/inspect argument followed by path to the script to debug. 
   ex) node inspect myscript.js
   Insert the statement debugger; into the source code of a script will enable a breeakpoint at that position in the code.

### 9. Difference between setImmediate() vs process.nextTick()

   **setImmediate()** : designed to queue the function behind whatever I/O event callbacks that are are already in the evnet queue.  

   **process.nextTick** : designed to effectively queue the function at the head of the event queue so that it executes immeidiately
   afther the current function complets.
   So in a case where you're trying to break up a long running, CPU-bound job using recursion, you would now want to use
   setImmeidate rather than process.nextTick to queue the next iteration as otherwise any I/O event callbacks wouldn't get the 
   chance to run between iterations.

### 10. What is libuv ?

   libuv is a multi-platform support library with a focus on asynchronous I/O. It was primarily developed for use by Node.js, but
   it's also used by Luvit, Julia, pyruv and others.

### 11. What is EventEmitter in Node.js ?

   All objects that emil events are instances of the EventEmitter class. These objects expose an eventEmitter.on() function
   that allows one or more functions to be attached to named events emitted by the object.
   When the EventEmitter object emits an event, all of the functions attached to that specific event are callsed synchronously.

  ![Event Loop diagram](/assets/img/posts/eventEmitter.png)

### 12. What is Streams in Node.js ?

   Streams are pipes that let you easily read data form a source and pipe it to a destincation. Simply put,
   a steram is nothing but and EventEmitter and implements some specials methods. Depending on the methods implements,
   a stream becomes Readable, Writable, Duplex and Transform.

   For example, if we want to read data from a file, the best way to do it from a stream is to listen to data event
   and attach a callback. When a chunk of data is available, the readable steram emits a data event and your callback
   executes.

  ![Event Loop diagram](/assets/img/posts/streams.png)

### 13. What is the difference between readFile vs createReadStream in Node.js ?

   **readFile** : is for asynchronously reads the entire contents of a file. It will read the file completely into memory before
   making it available to the User.  
   **readFileSync** : is synchronous version of readFile.
   createReadStream : It will read the file in chunks of the default size 64 kb which is specified before hand.

### 14. What is crypto in Node.js ? How do you cipher the secured information in Node.js ?

   The crypto module in Node.js provides cryptograpic functionality that includes a set of wrappers for OpenSSL's hash,
   HMAC, cipher, decipher, sign and verify functions.

  ![Event Loop diagram](/assets/img/posts/crypto.png)

### 15. What is the use of DNS module in Node.js?

   dns module which provide underlying system's name resolution and DNS look up facilities.
   DNS module consists of an asynchronous network wrapper.
  - dns.lookup(address, options, callback) : returns the corresponding IPV4 or IPV6 record according to options.
  - dns.lookupservice(address, port, callback) : converts any physical address such as 'www.medium.com' to array of record types.
  - dns.getServers() : returns an array of IP address strings, formatted according to rfc5952. that are currently configured fo DNS resolution.
  - dns.setServers() : set the IP address and port of servers to be used when performing DNS resolution.

### 16. What is a Callback function ?

   A callback is a function called at the completion of a given task. This prevents any blocking and allow other code to be run in the meantime.

  ![Event Loop diagram](/assets/img/posts/callback.png)

### 17. What are the security mechanisms available in Node.js ?

   **1. Authentication**  
   Authentication is one of the primary security states at which user is identified as permitted to access the application at all.
  - session-based authentication : the user's credentials are compared to the user account stored on the server and, in the vent of successful 
    validation, a session is started for the user. When the session expires, the user need to log in again.
  - token-based authentication : the user's credentials are applited to generate a string called a token which is then associated with the user's
  request to the server

   **2. Error Handling**  
   Usually, the error message contains the explanation of what’s actually gone wrong for the user to understand the reason. At the same time, 
   when the error is related to the application code syntax, it can be set to display the entire log content on the frontend. For an experienced hacker, 
   the log content can reveal a lot of sensitive internal information about the application code structure and tools used within the software.

   **3. Request Validation**  
   Another aspect which has to be considered, while building a secure Node.js application, is a validation of requests or, in other words, 
   a check of the incoming data for possible inconsistencies. It may seem that invalid requests do not directly affect the security of
   a Node.js application, however, they may influence its performance and robustness. Validating the incoming data types and formats and 
   rejecting requests not conforming to the set rules can be an additional measure of securing your Node.js application.

   **4. Node.js Security Tools and Best Practices**  
   We can use tools like helmet (protects our application by setting HTTP headers), csurf (validates tokens in incoming requests and rejects the invalid ones), 
   node rate limiter (controls the rate of repeated requests. This function can protect you from brute force attacks) and 
   cors (enables cross-origin resource sharing)

### 18. What is the passport in Node.js ?

   Passport.js is a simple, unobtrusive Node.js authentication middleware for Node.js. Passport.js can be dropped into any Express.js-based web application.
   Passport recognizes that each application has unique authentication requirements. Authentication mechanisms, known as strategies, are packaged 
   as individual modules. Applications can choose which strategies to employ, without creating unnecessary dependencies.

   By default, if authentication fails, Passport will repond with a 401 Unauthrized status, and any additional route handlers will not be invoked.
   If authentication succeeds, the next handler will be invoked and the req.user property will be set to the authenticated user.

### 19. What is express.js ?

   Express is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications.
   Express is a light-weight web application framework to help organize our web application into a MVC architecture on the server side. We can use
   a variety of choices for your templating language like EJS, Jade.
   Express.js basically helps you manage everything from routes to handling requests response and views.

### 20. What is middlewares ?

   Middleware functions are functions that have access to the request object, the response object and the next middleware function in the application's
   request-response cycle. The next middleware function is commonly denoted by a variable named next.  
   Middleware functions can perform the following tasks:
   - Execute any code.
   - Make changes to the request and the response objects.
   - End the request-response cycle.
   - Call the enxt middleware function in the stack.  
   Bind application-level middleware to an instance of the app object by using the **app.use()** and **app.method()** functions, where method is the 
   HTTP method of the request that the middleware function handles (such as GET, POST, PUT, DELETE) in lowercase.

   ![Middlewares](/assets/img/posts/middlewares.png)

### 21. What is Child Process and Cluster ? What are the difference ?

   **Child Process** in Node.js is used to run a child process under Node.js. There are two methods to do that: **exec** and **spawn**. The example for **exec**
   is:

   ![Middlewares](/assets/img/posts/childprocess_exec.png)

   We are passing our command as our first argument of the **exec** and expect three response in the callback. _stdout_ is the output we could expect from
   the execution.  
   *Cluster* is used to split a single process into mutiple processes or workers in Node.js terminology. This can be achieved through a cluster module.
   The cluster module allows you to create child processes(workers) which share all the server ports with the main Node process (master).  
   A cluster is a pool of similar workers running under a parent Node process. Workers are spawned using the fork() method of the child_processes module.
   Cluster is multiple processes to scale on multi cores.



   