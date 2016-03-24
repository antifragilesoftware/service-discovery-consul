# Service Discovery with Consul

Sample code for how to use Consul to do reasonably fault-tolerant service discovery between two services.

## Prerequisites

Please ensure you have a working Docker environment on your local machine. Instructions for how to achieve this for your own platform are available from the [Docker site](https://docs.docker.com/engine/installation/).

To build the Spring Boot microservices it is recommended that you have at least Java 1.8+ installed.

## Building the Services

Both services are currently implemented using Spring Boot and are then packaged into Docker images. The instructions for building the individual services are available in the corresponding service directories:

* [Simple Boot Microservice](sample-services/simple-boot-microservice)
* [Simple Boot Microservice Consumer](sample-services/simple-boot-microservice-consumer)

## Running the Services

Two runtime configurations are available, single-node and cluster. These refer to the fault-tolerancy of the consul and microservice runtime instances.

To run up thew services in one of these configurations simply change directory to the single-node or cluster directories and execute the following command:

`> docker-compose up -d`

To close the services down, simply execute the following command:

`> docker-compose down`




