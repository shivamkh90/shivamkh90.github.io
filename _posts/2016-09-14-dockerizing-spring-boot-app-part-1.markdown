---
layout: post
title:  "Dockerizing a spring boot app - Part 1"
date:   2016-09-13 13:35:00 +0530
categories: blogs java docker spring-boot
image: /assets/images/docker.png
linkText: Read More
tags: [Java, Docker, Spring Boot, Spring, Docker Images]
comments: true
disqus_identifier: 4
---


![Docker Logo]({{site.url}}/assets/images/docker.png "Docker"){:style="align:center;"}

Docker is an open-source initative to automate build and deploy processes on linux based platforms. The softwares build over docker run in software-containers over a host os. These software containers are isolated from each other by using cgroups or user namespaces feature available on linux platforms. According to the official [website](https://www.docker.com/what-docker), the features of docker are :-

> Docker containers wrap a piece of software in a complete filesystem that contains everything needed to run: code, runtime, system tools, system libraries – anything that can be installed on a server. This guarantees that the software will always run the same, regardless of its environment.

In essence it can be thought of an ultra-light replacement of server virtualization techniques.

##### Docker, the Commands we use most

Docker comes with a command line client to interact with the `docker` daemon. Below are some of them to let you work with docker as soon as possible :-

- `pull` :- It is used to pull/download images from docker repository for instance `docker pull java:8` will download an image with name `java` and tag `8` from the docker [hub](https://hub.docker.com/).
- `build` :- It is used to build an image from a `Dockerfile` for instance `docker build -t sample-build .` will build a docker image from a `Dockerfile` residing in the current directory.
- `run` :- Will run a docker image `docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres`. The preceding command will run a docker container with name `some-poostgres` from an image with name `postgres`. If the image doesn't exists on the local machine, docker will download and then run the image.
- `start` :- Starts a stopped container. eg: `docker start some-postgres`
- `stop` :- Stops a running container. eg: 'docker stop some-postgres'
- `exec` :- Runs a command in a running container for instance `docker exec -it some-postgres bash`. The preceeding command will run a `bash` shell in `-i` interactive mode in a container with name `-t` some-postgres.
- `push` :- Push/Upload the image to a docker registry. eg: `docker push testApp:1.0`

*For all the developers who might be confused with the terms image and container, Think of them as image being a class definition and container being an instance of that class. So you may create multiple containers from the same image.*

To get going, you can install docker by following instructions from this page :-
https://docs.docker.com/engine/installation/

In the next part i will be creating a `Dockerfile` to generate an image from our spring boot app from command line and probably a gradle way of doing it.


Thanks for reading, see you next time.
