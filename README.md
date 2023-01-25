
# BUILDING BUILD DEPENDENCIES

## Example Explanation

### Question
*How might we* use assets built in a different module as build dependencies?

### Why
You have some assets built in one module you would like to make availale to one
or more pods, such as libraries, fixtures, utilties, protocol buffers, etc.

### How
Use a garden task to retrieve the artifacts, the a task in an exec mdule to copy them into it's ony build directory, which can then be accessed byway of build dependencies in any module that want these assets.

### Steps
1. Create a container module to build the assets 
1. Create an exec module with a task to copy the assets into it's build directory
1. Create a container module that copies the assets using build dependencies
1. Create an `update-lib` custom command to make it easy for devs to run the task
1. Create a workflow that runs the task and deploys for CI

## Running Example

### Requires

- minikube

### For Developers

#### Command
`garden update-lib`

#####  Expected Result
- task `copy-lib-artifacts` runs and copies lib-artifcats into build directory

#### Command
`garden deploy`

##### Expected Result
- app is deployed with assets from lib-artifacts

#### Command
`garden test-lib`

##### Expected Result
- test script from lib-artifacts runs from app container

### For CI

#### Command
`garden run workflow deploy --env default`

#####  Expected Result
- runs `copy-lib-artifacts` and deploys app


## See
- [lib/Dockerfile](lib/Dockerfile)
- [lib/garden.yml](lib/garden.yml)
- [app/Dockerfile](app/Dockerfile)
- [app/garden.yml](app/garden.yml)
- [https://docs.garden.io/using-garden/tasks](https://docs.garden.io/using-garden/tasks)
- [https://docs.garden.io/guides/container-modules](https://docs.garden.io/guides/container-modules)
- [https://docs.garden.io/reference/module-types/exec](https://docs.garden.io/reference/module-types/exec)
- [https://garden.io](https://garden.io)
