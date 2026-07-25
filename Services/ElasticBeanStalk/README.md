# Elastic Beanstalk

### Use: to deploy and scale web apps more easily
* setup infrastructure for applications
    * setup load balancers
    * provision EC2 instances, S3 buckets, DynamoDB tables, etc
    * setup cloudwatch for monitoring and troubleshooting
* install and manage application stack on provisioned infrastructure
    * patches, updates to OS

### Supported Tech
* Languages: Java, .NET, PHP, Node.js, Python, Ruby, Go
* Platforms: Apache Tomcat, Docker

## Deploying Updates

### Main Approaches
* All at once: deploy to all hosts concurrently
* Rolling: deploy new version in batches, and each batch is taken out of service as deployment takes place
* Rolling with additional batch: launch an additional batch of instances, then deploys the new version in batches
* Immutable: deploy new version to fresh group of instances, then delete old instances once the new ones pass health checks 
* Traffic splitting: install new version of application on new instances, then forwards a portion of the client traffic to the new instances
    * allows you to evaluate app in production before fully commiting

### All at Once
* Pros:
    * relatively quick and simple
    * can work in dev environment
* Cons:
    * total outage while deployment takes place (not good for mission critical apps, or apps need to be 24/7)
    * if updates fails, you need to immediately rollback by redeploying original instances to all instances
        * this causes yet another outage

### Rolling Deployment
* can be done with Elastic Beanstalk
* Pros:
    * won't cause outage
* Cons:
    * environment capacity reduced by the number of instances in a batch during deployment
    * not good for performance sensitive systems
    * if update fails, you need to do another rolling update to change back the version

### Rolling with Additional Batch
* Pros:
    * no outage
    * maintain full capacity during deployment
    * if you need to rollback, no additional performance degradation during the rolling updates
* Cons: 
    * rollback still takes a lot of time that may not be suitable to performance sensitive systems

### Immutable
* Pros:
    * no outage, full capacity during deployment
    * if update fails, you can easily delete the new instances which makes rollback immediate
    * preferred for mission critical systems
* Cons:
    * 

### Traffic Splitting
* Pros:
    * can combine with immutable deployment
    * enables canary testing
        * intall new version on a new set of instances just like an immutable deployment
        * forward some of the incoming client traffic to the new application version during the evaluation period

## Configuration Setup

### Pre-Amazon Linux 2 Environments
* Use configuration file (.config) inside folder `.ebextensions` in top-level directory of application source code
    * format: yaml, json
    * specifies packages to install, linux users and groups to create, shell commands to run, services to enable, load balancers

Examples:
```
{
    "option_settings": [
        {
            "namespace": "aws:elasticbeanstalk:application",
            "option_name": "App healthcheck url"
            "value": "/healthcheck
        }
    ]
}
```

### Amazon Linux 2
* use Buildfile, Procfile, and platform hooks for configs
* use **Buildfile** for short-runned commands that then exit upon completion
    * e.g running a shell script for environment initialization
    * in root directory of app source code
* **Procfile** for long running application processes
    * e.g commands to start and run application
    * in root directory of application source code
    * processes defined here will run continuously; Elastic beanstalk will monitor and restart any processes that terminate
* **Platform hooks**: for custom scripts or execution files that can be run at chosen stage of EC2 provisioning process
    * stored in specific directories:
        * `.platform/hooks/prebuild`: files EBS runs before it builds, sets up, and configures application and web server
        * `.platform/hooks/predeploy`: files EBS runs after it sets up and configures application, but before it deploys them to the final runtime location
        * `.platform/hooks/postdeploy`: files that run after EBS deploys the application

## RDS Integration

### RDS within Elastic Beanstalk
* create RDS instance within elastic beanstalk environment
* If you terminate environment, database is also terminated
* probably better in dev environment for proof on concept
* not as suitable for apps in production

### RDS outside of Elastic Beanstalk
* create RDS in RDS console or AWS CLI
* lets you tear down elastic beanstalk environment without affecting database
* preferred for production systems
* additional requirements so that app in elastic beanstalk can connect to RDS:
    * security group for environment's autoscaling group to allow app to communicate with RDS from a port
    * need to add `RDS_HOSTNAME`, `DB_PASSWORD` in elastic beanstalk environment properties

## Migrating Apps to Elastic Beanstalk
* .NET apps: Windows web application migration assistant