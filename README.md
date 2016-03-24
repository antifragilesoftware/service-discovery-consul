# Service Discovery with Consul

Sample code for the [Antifragile Software](https://leanpub.com/antifragilesoftware) book that shows how to use Consul to do reasonably fault-tolerant service discovery between two services.

## Prerequisites

To run the services please ensure you have a working Docker environment on your local machine. Instructions for how to achieve this for your own platform are available from the [Docker site](https://docs.docker.com/engine/installation/).

To build the Spring Boot microservices it is recommended that you have at least Java 1.8+ installed.

## Running the Sample Services

Two runtime configurations are available, single-node and cluster. These refer to the fault-tolerancy of the consul and microservice runtime instances.

To run up thew services in one of these configurations simply change directory to the single-node or cluster directories and execute the following command:

`> docker-compose up -d`

To close the services down, simply execute the following command:

`> docker-compose down`

## (Optional) Building the Services

The services are already built and so can be retrieved from DockerHub, but if you'd like to build them yourself here's how you do that.

Both services are currently implemented using Spring Boot and are then packaged into Docker images. The instructions for building the individual services are available in the corresponding service repositories:

* [Simple Boot Microservice](https://github.com/antifragilesoftware/simple-boot-microservice)
* [Simple Boot Microservice Consumer](https://github.com/antifragilesoftware/simple-boot-microservice-consumer)


## Inspecting Consul fror Service Registration

Once your docker containers are running you can inspect Consul to see what services are registered and how they are clustered etc.

First you need to know what host your docker compose is running on. On my machine I simply open a new Docker Quickstart Terminal and the ip address of the docker host is displayed as shown below:

````
                        ##         .
                  ## ## ##        ==
               ## ## ## ## ##    ===
           /"""""""""""""""""\___/ ===
      ~~~ {~~ ~~~~ ~~~ ~~~~ ~~~ ~ /  ===- ~~~
           \______ o           __/
             \    \         __/
              \____\_______/


docker is configured to use the default machine with IP 192.168.99.100
For help getting started, check out the docs at https://docs.docker.com
```

I can now hit the following URL to inspect Consul:

`http://192.168.99.100:8500/ui`

***You will need to replace the ip address above with whatever ip your docker host is running on.*** For example:

`http://<your-docker-host>:8500/ui`

You can inspect your running services and service instances in the "Services" item in the Consul UI menu.

## Hitting the Outward-Facing Microservice

The microservice consumer is our entry-point to inspecting our running services themselves. If you hit the following URL you will be able to see your running microservice consumer:

`http://<your-docker-host>:8090`

On my machine as I write this, this interprets to:

`http://192.168.99.100:8090/`

All good so far. To see the status of consul connections and hystrix circuit-breaker and client-side load balancing status and other health metrics about your service just hit the `health` endpoint instead:

`http://<your-docker-host>:8090/health`

On my machine as I write this, this interprets to:

`http://192.168.99.100:8090/health`

Finally hit the following URL to see all the client-side load-balanced microservices that have been discovered:

`http://<your-docker-host>:8090/discoveredServiceInstances`

On my machine as I write this, this interprets to:

`http://192.168.99.100:8090/discoveredServiceInstances`

## Getting Antifragile by Stressing the System

One simple stressor is service failure. Services can come and go in the real world and so we should model that as a known-stressor in our system. For ideas on how you can try out these stressors check out the [stressors](stressors) directory.



 
