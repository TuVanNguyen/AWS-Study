# Lambda

## Cost (pay by use)
* Requests: $0.20 per 1M requests each month
* Duration: charged in 1 millisecond increments based on memory allocated to lambda function
* price per GB second 
    * if you have a function that uses M GB of memory and runs for T milliseconds, you pay $Price * M * T$

## Triggers
* Event driven Architecture: lambda functions can be automatically triggered by events in S3 or DynamoDB (e.g adding or changing a record in a table)
    * can be triggered by many [other services too](https://aws.amazon.com/blogs/architecture/understanding-the-different-ways-to-invoke-lambda-functions/)
* Triggered by user requests: use API gateway to configure an http endpoint to trigger function with HTTP request


### Limits
* Concurrent Execution limit: limit number of concurrent executions across all functions in a given region per account
    * Default: 1000 per region
    * Error in logs: `TooManyRequestsException`
    * HTTP Status Code: 429
    * Error Message: "Request thoroughput limit exceeded"
    * Common Signs Limit is exceeded:
        * having many lambda functions running in same region and you suddenly see new invocation requests being rejected
    * Solutions:
        * make request to AWS Support Center to increase limit
        * Configure *reserved concurrency*: guarantees set number of executions will always be available for critical functions