---
title: "Docker Keywords"
date: 2021-10-23 00:07:00 +0900
classes: wide
tags:
    - tech
    - computer
---

## Keywords
- Operating System Level Visualization
- Container
- Single OS kernel
- Difference with Virtual Machines
    - Docker Containers. Fast! Light!
        - Rely on the underlying OS kernel
        - Containers share resources with other containers in the same host OS
        - OS-level process isolation
    - Virtual Machines
        - Run on Hypervisors, which allow multiple Virtual Machines to run on a single machine along with its own operating system
        - Hardware-level process isolation
- Docker Image : It is a file, comprised of multiple layers, used to execute code in a Docker container.
- Docker Container : runtime instance of an image
- Dockerfile : text document that contains necessary commands which on execution helps assemble a Docker Image
- Docker Engine: The Software that hosts the containers.
    - Server : managing Images, Containers, Networks, and Volumes on the Docker
    - REST API : how the applications can interact with the Server and instructs it what to do
    - Client : docker command-line interface.
- Docker Hub : online repository where you can find other Docker Images.