# Dockerize a Django Application

This guide demonstrates how to use docker and docker compose to setup and run a simple Django/PostgreSQL application.

## Getting Started

For this project we need to have a Dockerfile,a python dependencies (requirements.txt),and docker-compose.yml file.### Prerequisites

Having Docker and Docker Compose installed.

```
Give examples
```

### Download the sample 

In a terminal window, run the following command to clone the sample app repository to your local machine, then change to the directory that contains the sample code.

```
git clone https://github.com/Taddist/Docker_Django.git
cd Docker_Django
```

## Create Docker Image

In the Git repository, take a look at Dockerfile. This file describes the Python environment that is required to run the application. 

The file requirements.txt include basic requirements to start and deploy our Django application.

To build the Docker image , run the docker build command 


