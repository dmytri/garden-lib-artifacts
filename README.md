
# BUILDING BUILD DEPENDENCIES

## Example Explanation

### Question
*How might we* use assets built in a different module as build dependencies?

### Why
You have some assets built in one module you would like to make availale to one
or more other modules, such as libraries, fixtures, utilties, protocol buffers, etc.

### How
Use a garden task to retrieve the artifacts from the container, thne a task in an exec mdule to copy them into it's own build directory which can then be accessed byway of build dependencies in any module that needs these assets.

### Steps
1. Create a container module to build the assets 
1. Create a tast to retrieve the artifacts
1. Create an exec module with a build command to run above task and copy the assets into it's build directory
1. Create a container module that includes the exec module as a build dependencies
1. Create an `test-lib` custom command to make run the test script from the app container

## Running Example

### Requires

- minikube

#### Command
`garden deploy`

##### Expected Result
- app is deployed with assets from lib-artifacts

#### Command
`garden test-lib`

##### Expected Result
- test script from lib-artifacts runs from app container

## See
- [lib/Dockerfile](lib/Dockerfile)
- [lib/garden.yml](lib/garden.yml)
- [app/Dockerfile](app/Dockerfile)
- [app/garden.yml](app/garden.yml)
- [https://docs.garden.io/using-garden/tasks](https://docs.garden.io/using-garden/tasks)
- [https://docs.garden.io/guides/container-modules](https://docs.garden.io/guides/container-modules)
- [https://docs.garden.io/reference/module-types/exec](https://docs.garden.io/reference/module-types/exec)
- [https://garden.io](https://garden.io)
