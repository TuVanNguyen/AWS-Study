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

### Features
* support multiple endpoints and targets
* supports multiple versions of API (e.g dev, qa, prod)
* serverless
* integrates with Cloudwatch: logs API calls, latencies, error rates
* throttling: manage traffic with throttling so backend apps protected against traffic spikes and DoS attacks (Denial of Service)

### Supported Types
* RESTful APIs: optimized for stateless, serverless workloads
* Websocket APIs: real-time, two-way, stateful communication e.g chat apps



