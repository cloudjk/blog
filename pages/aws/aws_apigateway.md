---
title: AWS API Gateway
sidebar: mydoc_sidebar
permalink: aws_apigateway.html
folder: aws
---


### API Gateway Overview

#### Building a Serverless API
  - {% include image.html file="serverless_api.png" %}

#### API Gateway
  - AWS Lambda + API Gateway: **No infrastructure to manage**
  - Support for the WebSocket Protocol
  - Handle API version (v1, v2...)
  - Handle different environments (dev, test, prod...)
  - Handle security (Authentication and Authorization)
  - Create API keys, handle request throttling
  - Swagger / Open API import to quickly define APIs
  - Transform and validate requests and responses
  - Generate SDK and API specifications
  - Cache API responses

#### Integrations High Level
  - Lambda Function
    - Invoke Lambda function
    - Easy way to expose REST API backed by AWS Lambda
  - HTTP
    - Expose HTTP endpoints in the backend
    - Example: internal HTTP API on premise, Application Load Balancer...
    - Why? Add rate limiting, caching, user authentications, API keys, etc...
  - AWS Service
    - Expose any AWS API through the API Gateway?
    - Example: start an AWS Step Function workflow, post a message to SQS
    - Why? Add authentication, deploy publicly, rate control...

#### Endpoint Types
  - Edge-Optimized (default): For global clients
    - Requests are routed through the CloudFront Edge locations (improves latency)
    - The API Gateway still lives in only one region
  - Regional:
    - For clients within the same region
    - Could manually combine with CloudFront (more control over the caching strategies and the distribution)
  - Private:
    - Can only be accessed from you VPC using an interface VPC endpoint (ENI)
    - Use a resource policy to define access

### API Gateway - Stages and Deployment
  
#### Deployment Stages
  - Making changes in the API Gateway does not mean they're effective
  - You need to make a "deployment" for them to be in effect
  - It's a common source of confusion
  - Changes are deployed to "Stages" (as many as you want)
  - Use the naming you like for stages (dev, staging, prod)
  - Each stage has its own configuration parameters
  - Stages can be rolled back as a history of deployments is kept

#### Stages v1 and v2
  - {% include image.html file="api_v1_v2.png" %}

#### Stage Variables
  - Stage variables are like **environment variables for API Gateway**
  - Use them to change often changing configuration values
  - They can be used in:
    - Lambda function ARN
    - HTTP Endpoint
    - Parameter mapping templates
  - Use cases:
    - Configure HTTP endpoints your stages talk to (dev, staging, prod ...)
    - Pass configuration parameters to AWS Lambda through mapping templates
  - Stage variables are passed to the "context" object in AWS Lambda

#### Canary Deployment
  - Possibility to enable canary deployments for any stage (usually prod)
  - Choose the % of traffic the canary channel receives
  - {% include image.html file="canary_deployment.png" %}
  - Metrics & Logs are separate (for better monitoring)
  - Possibility to override stage variables for canary
  - This is blue/green deployment with AWS Lambda & API Gateway

### API Gateway Integration Types & Mappings

#### Integration Types
  - Integration Type MOCK
    - API Gateway returns a response without sending the request to the backend
  - Integration Type HTTP/AWS (Lambda & AWS Services)
    - You must configure both the integration request and integration response
    - Setup data mapping using **mapping templates** for the request & response
    - {% include image.html file="integration_type_http_Aws.png" %}
  - Integration Type AWS_PROXY (Lambda Proxy):
    - Incoming request from the client is the input to Lambda
    - The function is responsible for the logic of request/response
    - No mapping template, headers, query string parameters ... are passed as arguments
    - {% include image.html file="aws_proxy.png" %}
  - Integration Type HTTP_PROXY
    - No mapping template
    - The HTTP request is passed to the backend
    - The HTTP response from the backend is forwarded by API Gateway
    - {% include image.html file="http_proxy.png" %}
    
#### Mapping Template (AWS & HTTP Integration)
  - Mapping templates can be used to modify request / responses
  - Rename / Modify query string parameters
  - Modify body content
  - Add headers
  - User Velocity Template Language (VTL): for loop, it etc...
  - Filter output results (remove unnecessary data)

#### Mapping Example: JSON to XML with SOAP
  - SOAP API are XML based, whereas REST API are JSON based
    - {% include image.html file="json_xml.png" %}
  - In this case, API Gateway should:
    - Extract data from the request: either path, payload or header
    - Build SOAP message based on request data (mapping template)
    - CALL SOAP service and receive XML response
    - Transform XML response to desired format (like JSON) and respond to the user

#### Mapping Example: Query String parameters
  - {% include image.html file="query_string_parameters.png" %}

### API Gateway Caching

#### Caching API Responses
  - Caching reduces the number of calls made to the backend
  - Default TTL (time to live) is 300 seconds (min: 0s, max: 3600s)
  - Caches are defined per stage
  - Possible to override cache settings per method
  - Cache encryption option
  - Cache capacity between 0.5GB to 237GB
  - Cache is expensive, make sense in production, may not make sense in dev / test
  - {% include image.html file="caching_api.png" %}

#### Cache Invalidation
  - Able to flush the entire cache(invalidate it) immediately
  - Clients can invalidate the cache with **header:Cache-Contro:max-age=0** (with proper IAM authorization)
  - If you don't impose an InvalidateCache policy (or choose the Require authorization check box in the console), any client can invalidate the API cache
  - {% include image.html file="api_gw_cache.png" %}

### API Gateway Usage Plans & API Keys

#### Overview
  - If you want to make an API available as an offering ($) to your customers
  - Usage Plan:
    - who can access one or more deployed API stages and methods
    - how much and how fast they can access them
    - uses API keys to identify API clients and meter access
    - configure throttling limits and quota limits that are enforced on individual client
  - API Keys:
    - alphanumeric string values to distribute to your customers
    - Can use with usage plans to control access
    - Throttling limits are applied to control access
    - Quotas limits is the overall number of maximum requests

#### Correct Order for API keys
  - To configure a usage plan
    - 1. Create one or more APIs, configure the methods to require an API key, and deploy the APIs to stages
    - 2. Generate or import API keys to distribute to application developers (your customers) who will be using your API
    - 3. Create the usage plan with the desired throttle and quota limits
    - 4. **Associate API stages and API keys with the usage plan**
  - Callers of the API must supply an assigned API key in the x-api-key header in requests to the API

### API Gateway Monitoring, Logging and Tracing

#### Logging & Tracing
  - CloudWatch Logs:
    - Enable CloudWatch logging at the Stage level (with Log Level)
    - Can override setting on a per API basis (e.g. Error, Debug, Info)
    - Log contains information about request / response body
  - X-Ray:
    - Enable tracing to get extra information about requests in API Gateway
    - X-Ray API Gateway + AWS Lambda gives you the full picture
  
#### CloudWatch Metrics
  - Metrics are by stage, Possibility to enable detailed metrics
  - CacheHitCount & CacheMissCount: efficiency of the cache
  - Count: The total number of API requests in a give period
  - Integration Latency: The time between when API Gateway relays a request to the backend and when it receives a response from the backend
  - Latency: The time between when API Gateway receives a request from a client and when it returns a response to the client. The latency includes the integration latency and other API Gateway overhead(e.g Authentication, Authorization, parameter mapping, caching..)
  - 4XXError (client-side) & 5XXError (server-side)

#### API Gateway Throttling
  - Account Limit
    - API Gateway throttles request at 10000 rps(request per second) across all API
    - Soft limit that can be increased upon request
  - In case of throttling => 429 Too Many Requests (re-triable error)
  - Can set **Stage limit & Method limits** to improve performance
  - Or you can define Usage Plans to throttle per customer
  - **Just like Lambda Concurrency, one API that is overloaded, if not limited, can cause other APIs to be throttled**

#### API Gateway - Errors
  - 4xx means Client Errors
    - 400: Bad Request
    - 403: Access Denied, WAF(Web Application File) filtered
    - 429: Quota exceeded, Throttle
  - 5xx means Server Errors
    - 502: Bad Gateway Exception, usually for an incompatible output returned from a Lambda proxy integration backend and occasionally for out-of-order invocations due to heavy loads
    - 503: Service Unavailable Exception
    - 504: Integration Failure - e.g. Endpoint Request Timed-out Exception (API Gateway requests time out after 29 second maximum)

### API Gateway - CORS (Cross-Origin Resource Sharing)

#### CORS Overview
  - CORS must be enabled when you receive API calls from another domain
  - The OPTIONS pre-flight request must contain the following headers:
    - Access-Control-Allow-Methods
    - Access-Control-Allow-Headers
    - Access-Control-Allow-Origin
  - **CORS can be enabled through the console**

#### CORS - Enabled on the API Gateway
  - {% include image.html file="cors.png" %}


### API Gateway - Security (Authentication & Authorization)

#### API Gateway - Permissions

  - Create an IAM policy authorization and attach to User/Role
  - **Authentication = IAM / Authorization = IAM Policy**
  - Good to provide access within AWS (EC2, Lambda, IAM users...)
  - Leverages "Sig 4" capability where IAM credential are in headers
  - {% include image.html file="iam_permission.png" %}

#### API Gateway - Resource Policies

  - Resource policies (similar to Lambda Resource Policy)
  - Allow for Cross Account Access (combined with IAM Security)
  - Allow for a specific source IP address
  - Allow for a VPC Endpoint
  - {% include image.html file="resource_policy.png" %}

#### API Gateway - Cognito User Pools

  - Cognito fully manages user lifecycle, token expires automatically
  - API Gateway verifies identity automatically from AWS Cognito
  - No custom implementation required
  - Authentication = Cognito User Pools | Authorization = API Gateway Methods
  - {% include image.html file="cognito_user_pools.png" %}

#### API Gateway - Lambda Authorizer (formerly Custom Authorizers)
  - Token-based authorizer (bearer token) - e.g. JWT or Oauth
  - A request parameter-based Lambda authorizer (headers, query string, stage var)
  - Lambda must return an IAM policy for the user, result policy is cached
  - Authentication = External | Authorization = Lambda function
  - {% include image.html file="lambda_authorizer.png" %}

#### API Gateway Security Summary
  - IAM:
    - Great for users / roles already within your AWS account, + resource policy for cross account
    - Handle authentication & authorization
    - Leverage Signature v4
  - Custom Authorizer:
    - Great for 3rd party tokens
    - Very flexible in terms of what IAM policy is returned
    - Handle Authentication verification + Authorization in the Lambda function
    - Pay per Lambda invocation, results are cached
  - Cognito User Pool
    - You manage your own user pool (can be baked by Facebook, Google login etc...)
    - No need to write any custom code
    - Must implement authorization in the backend

### API Gateway - HTTP API vs REST API
  - HTTP APIs
    - low-latency, cost-effective AWS Lambda proxy, HTTP proxy APIs and private integration (no data mapping)
    - support OIDC(Open ID Connect) and OAuth2.0 authorization and built-in support for CORS
    - No usage plans and API keys
  - REST APIs
    - All features (except Native OpenID Connect / OAuth 2.0)
  - {% include image.html file="http_rest.png" %} 

### API Gateway - WebSocket API

#### WebSocket API Overview
  - What is WebSocket?
    - Two-way interactive communication between a user's brwoser and a server
    - Server can push information to the client
    - This enables **stateful** application use cases
  - WebSocket APIs are often used in real-time applications such as chat applications, collaboration platforms, multiplayer games and financial trading platforms
  - Works with AWS Services (Lambda, DynamoDB) or HTTP endpoints
  - {% include image.html file="websocket_api_overview.png" %} 

#### Connecting to the API
  - WebSocket URL
  - wss://[some-unique-id].execute-api.[region].amazonaws.com/[stage-name]
  - {% include image.html file="websocket_url.png" %} 

#### Client to Server Messaging: **ConnectionID is re-used**
  - WebSocket URL
  - wss//abcdef.execute-api.us-west-1.amazonaws.com/dev
  - {% include image.html file="server_messaging.png" %} 

#### Server to Client Messaging
  - WebSocket URL
  - wss//abcdef.execute-api.us-west-1.amazonaws.com/dev
  - {% include image.html file="server_to_client_messaging.png" %} 

#### Connection URL Operations
  - Connection URL
  - wss//abcdef.execute-api.us-west-1.amazonaws.com/dev/@connections/connectionId
  - {% include image.html file="connection_url.png" %} 

#### WebSocket API Routing
  - Incoming JSON messages are routed to different backend
  - If no routes => sent to $default
  - You request a **route selection expression** to select the field on JSON to route from
  - Sample expression: $request.body.action
  - The result is evaluated against the route keys available in your API Gateway
  - The route is then connected to the backend you've setup through API Gateway
  - {% include image.html file="websocket_routing.png" %} 
