# CodeDeploy
automates deployment of EC2, on-prem, lambdas

### Pros
* quickly release new features
* avoid downtime during deployments
* avoid risks with manual processes

## Approaches

### In-place aka rolling update
1. CodeDeploy stops one of the instances
1. CodeDeploy install a new release, called a **revision**, on the stopped instance
1. CodeDeploy restarts the instance, then moves on to the next 
* To roll-back, you need to redeploy the previous version using the steps above
* Pros:
    * good for first-time deployment
* Cons:
    * instances will be out of service during deployment, so capacity is reduced
    * need to configure ELB to stop sending requests to out of service instances during deployment (can configure in CodeDeploy)
    * roll-back is not easy and time-consuming because it requires redeploying
    * doesn't support lambda deployments



### Blue-green
1. CodeDeploy provisions new "green" instances, then installs the new release on them
1. CodeDeploy registers the green instances with the elastic load balancer, and route traffic away from the "blue" instances
1. CodeDeploy terminates old blue instances
* roll-back: do before the blue instances are terminated, simply by rerouting ELB back to blue instances
* Blue: active deployment
* Green: new release
* Pros:
    * roll-back is relatively quick and easy to do immediately after deployment
    * no capacity reduction
    * overall the safest option for production environments
* Cons:
    * additional costs for keeping blue instances, until they're terminated

## AppSec File
* Configuration file for CodeDeploy deployment
    * YAML format only for EC2, on-prem services
    * YAML/JSON format for lambda
* defines parameters to be used by CodeDeploy: OS, files, hooks, etc


### Structure
* **version**: only allowed value is 0.0
* **OS**: operating system e.g linux, windows
* **files**: application files to copy onto instance
* **hooks**: scripts which need to run at set points in deployment; has specific run order
    * example scripts: unzip files, run tests, registering or deregistering instances with elastic load balancer

```
version: 0.0
os: linux
files:
    - source: Config/config.txt
      destination: /webapps/Config
    - source: Source
      destination /webapps/src
hooks:
    BeforeInstall:
        - location: Scripts/unzipApp.sh
    AfterInstall:
        - location: Scripts/RunResourceTests.sh
            timeout: 180
    ApplicationStart:
        - location: Scripts/setup.sh
        - location:  RunFunctionTests.sh
            timeout: 3600
    ValidateService:
        - location: Scripts/MonitorService.sh
            timeout: 3600
            runas: codedeployuser
```

### Typical Folder Setup
* appspec.yml: must be in root directory of revision
* /Scripts
* /Config
* /Source

### Lifecycle Event Hooks
1. De-registering instances from event balancer
    1. BeforeBlockTraffic hooks: run tasks that need to happen before de-registering instances
    1. BlockTraffic hooks: scripts relating to de-registering instances
    1. AfterBlockTraffic: tasks to run after instances are de-registered 
1. deploy application
    1. ApplicationStop: scripts to gracefully stop application 
    1. DownloadBundle: CodeDeploy copies application revision files to a temp location
    1. BeforeInstall: pre-install scripts e.g backup current version, decrypt files, decompress files
    1. Install: copy application revision files to final location
    1. AfterInstall: post-install scripts e.g configuration, file permissions
    1. ApplicationStart: start any services that were stopped during ApplicationStop
    1. ValidateService: run tests to validate service
1. re-register instances with load balancer
    1. BeforeAllowTraffic: tasks to run on instances before they're re-registered
    1. AllowTraffic: scripts to register instances with load balancer
    1. AfterAllowTraffic: tasks to run on instances after they are re-registered 


