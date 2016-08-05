Jenkins Docker Slave
====================

This repository contains a Jenkins Slave installation with the Swarm Plugin
that has access to docker and docker-compose commands.

Unlike other Jenkins with Docker images which use Docker in Docker (DIND)
it connects by default with the docker instance on the host and creates sister
containers.

A docker-compose file for this might look like this:
```
version: '2'
services:
  master:
    image: around25/jenkins-docker-slave
    restart: always
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      - COMMAND_OPTIONS=-master http://master.jenkins:8080 -name slave -username slave -password secret
    networks:
      default:
        aliases:
          - slave.jenkins
```
