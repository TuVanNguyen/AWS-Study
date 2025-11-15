# Cloudfront (Content Delivery Network)


### Why Use
* effectively deliver content to end users, with optimal performance
* optimized to work with other AWS services including S3, EC2, ELB, Route53
* works with non-AWS origin servers

## Terminology
* Cloudfront Edge Location: where content is cached (typically closest to location where content was requested)
    * > 200 edge locations in network around the world
* Cloudfront Origin: origin of content the distribution will serve e.g s3 bucket, ec2 instance, elastic load balancer, or route 53
* Cloudfront Distribution: name given to origin and config settings for content you want to distribute with Cloudfront
* TTL (Time to Live): time objects are cached at edge locations (default 1 day)
    * you'll be charged for clearing cache before TTL is up

### S3 Transfer Acceleration
* enables fast, secure transfers of files between end users from edge locations to s3 bucket


## Allowed Methods

* What?: the http methods you choose your cloudfront distribution to work

| Mode | Methods |
|------|---------|
|Read only | GET, HEAD, [OPTIONS] |
| Read and Write | GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE |

| Supported HTTP Methods | Definition | Example |
|------------------------|------------|---------|
| GET | read data, often default used by http clients | read or see a webpage |
| HEAD | Inspect resource headers; similar to GET, except without the response body | read web page's header |
| PUT | create or replace an existing resource; idempotent | update profile|
| PATCH | partially modify a resource | modify contents of shopping cart |
| POST | Insert data; create or update a resource; not idempotent | comment on a blog post |
| DELETE | delete data | remove email from mailing list |
| OPTIONS | find out what other HTTP methods are supported by given url | get list of supported HTTP methods |


* Idempotent: if we send exact same request multiple times, the response is always the same and change in state is the same
