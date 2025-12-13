# API Gateway

### Basic Concepts
* API: Application Programming Interface
    * allows users to interact with web apps (by interfacing between the front-end and back-end)
    * allows apps to communicate to each other
* RESTful APIs: REpresentational State Transfer
    * Stateless: nothing is persisted in the app or API itself
    * support JSON (JavaScript Object Notation): uses key-value pairs
* API Gateway: single endpoint for all client traffic interacting with backend of apps


## What is API Gateway on AWS?
* service that publishes, maintain, monitor, and secure APIs at any scale

## Features
* support multiple endpoints and targets
* supports multiple versions of API (e.g dev, qa, prod)
* serverless
* integrates with Cloudwatch: logs API calls, latencies, error rates
* throttling: manage traffic with throttling so backend apps protected against traffic spikes and DoS attacks (Denial of Service)
* import APIs into API Gateway using API Definition files (supported protocols: OpenAI(formerly Swagger))

### Caching
* cache endpoint response to reduce number of calls to endpoint and improve latency
* TTL (time to live): time to keep response in cache; default: 300 seconds (5 minutes)

### Throttling
* to prevent overwhelming API with too many requests
* default steady-state request rate: 10,000 requests per second, per region
* maximum concurrent requests: 5,000 requests across all APIs per region
* can request increase on limit for the two above
* if you do exceed the request rate and concurrent request limit, you will get **429 Too Many Requests** error

### Supported Types
* RESTful APIs: optimized for stateless, serverless workloads
* Websocket APIs: real-time, two-way, stateful communication e.g chat apps
* Legacy applications:
    * SOAP: 
        * configure API Gateway as SOAP web service passthrough
            * response is passed back to client as XML
        * use API Gateway to transform XML to JSON

### Mock endpoints aka mock integration
* simulates responses from a real API, allowing devs to create, test, and debug
* good to test front-end components when backend isn't ready

## API Stage
* references lifecycle state of API e.g dev, qa, prod, v3
* each stage can be associated with different endpoint
* each stage has unique invoke url e.g http://abcd.execute-api.us-east-1.amazonaws.com/**dev**

### Stage Variables
* key-value pairs that act as environment variables
* can use to define backend endpoint (e.g lambda)

## API Request and Response Transformations

### Parameter Mapping
* used to modify API requests and responses
* in requests, we can change header, query string, request path
* in responses, we can change header, status code, 





