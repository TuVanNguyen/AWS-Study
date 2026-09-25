# CodePipeline
* orchestrates end-to-end software release based on a workflow you define
* automated release process, CICD service
    * pipeline triggered every time there's a code change pushed

### Pros:
* fast, quick releases
* consistent, so less prone to errors during deployment

### Integrations
* AWS Developer Tools: CodeCommit, CodeBuild, CodeDeploy, 
* Opensource Tools: Github, Jenkins
* Other AWS: EBS, Cloudformation, Lambda, ECS

### Process
1. CodeCommit: New code detected in repo
1. CodeBuild: immediately compiles source code, run tests, and produce packages/artifacts
1. CodeDeploy: newly built app is deployed into staging or production environment


