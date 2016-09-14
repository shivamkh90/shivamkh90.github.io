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


![Docker Logo]({{site.url}}/assets/images/docker.png "Docker"){:style="display:block; margin: auto;"}

Docker is an open-source initative to automate build and deploy processes on linux based platforms. The softwares build over docker run in software-containers over a host os. These software containers are isolated from each other by using cgroups or user namespaces feature available on linux platforms. According to the official [website](https://www.docker.com/what-docker), the features of docker are :-

> Docker containers wrap a piece of software in a complete filesystem that contains everything needed to run: code, runtime, system tools, system libraries – anything that can be installed on a server. This guarantees that the software will always run the same, regardless of its environment.

In essence it can be thought of an ultra-light replacement of server virtualization techniques.

##### Docker, the Commands we use most

Docker comes with a command line client to interact with the <span class="icode">docker</span> daemon. Below are some of them to let you work with docker as soon as possible :-

- <span class="icode">pull</span> :- It is used to pull/download images from docker repository for instance <span class="icode">docker pull java:8</span> will download an image with name <span class="icode">java</span> and tag <span class="icode">8</span> from the docker [hub](https://hub.docker.com/).
- <span class="icode">build</span> :- It is used to build an image from a <span class="icode">Dockerfile</span> for instance <span class="icode">docker build -t sample-build .</span> will build a docker image from a <span class="icode">Dockerfile</span> residing in the current directory.
- <span class="icode">run</span> :- Will run a docker image <span class="icode">docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres</span>. The preceding command will run a docker container with name <span class="icode">some-poostgres</span> from an image with name <span class="icode">postgres</span>. If the image doesn't exists on the local machine, docker will download and then run the image.
- <span class="icode">start</span> :- Starts a stopped container. eg: <span class="icode">docker start some-postgres</span>
- <span class="icode">stop</span> :- Stops a running container. eg: <span class="icode">docker stop some-postgres</span>
- <span class="icode">exec</span> :- Runs a command in a running container for instance <span class="icode">docker exec -it some-postgres bash</span>. The preceeding command will run a <span class="icode">bash</span> shell in <span class="icode">-i</span> interactive mode in a container with name <span class="icode">-t</span> some-postgres.
- <span class="icode">push</span> :- Push/Upload the image to a docker registry. eg: <span class="icode">docker push testApp:1.0</span>

*For all the developers who might be confused with the terms image and container, Think of them as image being a class definition and container being an instance of that class. So you may create multiple containers from the same image.*

To get going, you can install docker by following instructions from this page :-
https://docs.docker.com/engine/installation/

In the next part i will be creating a <span class="icode">Dockerfile</span> to generate an image from our spring boot app from command line and probably a gradle way of doing it.


Thanks for reading, see you next time.
