# Step Functions

### What
* visual interface to build and run serverless apps as a series of steps


### How They Work
* automatically trigger and track each step
* output of one step is input for the next step 
* log state of each step to help with debugging


## Terms
* Task: single step, single unit of work
* State Machine: the entire workflow of tasks
    * defined using Amazon State Language
    * implemented as a Cloudformation stack

## Workflows

### Sequential Workflow

<img src="imgs/SequentialWorkflow.png" height="300">

* steps happen one after the other
* output of one step is input for the next step 
* each step is fulfilled by separate lambda functions
* "Decode base64 string" is a *task*
* Everything between Start and End is a *state machine*

### Parallel Workflow

<img src="imgs/ParallelWorkflow.png" height="300">

* These steps are running in parallel in separate lambda functions
    * "Extract metadata"
    * "Resize image"
    * "Facial Recognition"

### Branching Workflow

<img src="imgs/BranchingWorkflow.png" height="300">

* branches at "All Tests Passed?" task, which determines which lambda function to run
    * yes: run "Notify Success"
    * no: run "Notify Failure"

