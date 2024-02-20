# OpenMRS Clinical Data Repository ( Federation/Synchronization)
The attempt here is to create a central data repository that ensures FHIR-based synhronization of patient data between two instances of OpenMRS. The demonstrated communication workflow involves the following components:
- Master Patient Index (MPI)
- Shared Health Record (SHR)
- Two instances of OpenMRS

The communication between these systems utilizes the FHIR clinical data standard for representing clinical data, and is orchestrated by the OpenHIM middleware.

## Installation
### Install Docker
- Docker Engine: `https://docs.docker.com/compose/install/`
- Docker Compose: `https://docs.docker.com/compose/install/`

### Clone the CDR Repository
`git clone https://github.com/mherman22/openmrs-module-cdr.git`

### Pull all containers
`sudo docker-compose -f docker-compose.yml pull`

### Start up Core containers
```
sudo docker-compose -f docker-compose.yml up -d openhim-core openhim-console mongo-db
```

### Start up Openhim-config container to load configurations into the mediator
```
sudo docker-compose -f docker-compose.yml up openhim-config
```

### Start up shr-fhir opencr-fhir opencr-es
```
sudo docker-compose -f docker-compose.yml up -d shr-fhir opencr-fhir opencr-es
```

### Start up Client Registry and Shared Health Record
```
sudo docker-compose -f docker-compose.yml up -d shr opencr
```

### Start up the OpenMRS instances
 ```
sudo docker-compose -f docker-compose.yml up -d openmrs-db-mysql openmrs-facilityA
```
```
sudo docker-compose -f docker-compose.yml up -d openmrs-referenceapplication-mysql openmrs-referenceapplication
```

## login details for openhim-core 

```
username: root@openhim.org
password: Admin123
```

## Useful Docker commands
Below are a few useful Docker commands that will allow you to have better visibility into your OpenHIM/Docker setup.

### Check running processes
Now that we have our OpenHIM successfully created and running, we might need to check up on our Docker processes running to find some additional metadata on our containers. Execute the below command to find all the running Docker processes.

```
docker ps
```
### Access the Openhim core logs
To access the OpenHIM core logs, execute the below command within your terminal to see and follow (-f) the output of the container logs.

```
docker logs -f openhim-core
```
### Stop the Docker service

```
docker stop <container_name or container_id>
```

To stop all the running OpenHIM Docker services, we need to execute the below command.

```
docker stop $(docker ps -a)
```

### Inspect details of a container

```
docker inspect <container_name>
```

### List available Docker networks

```
docker network ls
```

### Access a terminal within a running container

```
docker exec -it <container_name> bash
```
