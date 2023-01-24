
# VOLUME SEEDING

## Example Explanation

### Question
*How might we* pre-seed a volume with some assets and make them available for services.

### Why
You have some assets you would like to make availale to one or more pods without needing to rebuild containers to update them.

### How
Use a garden task and a utility container to copy the assets to a volume

### Steps
1. Create a minimal Dockerfile with the assets
1. Create a garden task to mount the volume and copy the assets to it
1. make the task a dependency of the service that needs the assets

## Running Example

### Requires

- minikube

Note: this exampe uses the hostPath storage class that comes with minikube, so
this is a one node solution, to use in a real scenario with multiple nodes, a
distributed storage class would be required.

#### Command
`garden deploy`

#####  Expected Result
- task `seed-volume-lib` runs and seeds volume-lib
- service `app` is deployed with `volume-lib` mounted cotaining a test shell script

#### Command
`garden test-lib`

##### Expected Result
- test shell script is executed on `app` container

#### Command
`garden update-lib`
- task `seed-volume-lib` runs and updates volume-lib

##### Expected Result
- any modified or added assets in lib/src writen to `volume-lib`

## See
- [lib/Dockerfile](lib/Dockerfile)
- [lib/garden.yml](lib/garden.yml)
- [app/Dockerfile](app/Dockerfile)
- [app/garden.yml](app/garden.yml)
- [https://docs.garden.io/using-garden/tasks](https://docs.garden.io/using-garden/tasks)
- [https://docs.garden.io/guides/container-modules#mounting-volumes](https://docs.garden.io/guides/container-modules#mounting-volumes)
- [https://garden.io](https://garden.io)
