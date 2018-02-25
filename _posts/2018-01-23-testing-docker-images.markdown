---
layout: post
title:  "Testing Docker Images"
summary: "How to test your Docker images"
date:   2018-02-24 20:00:00
categories: coding
tags: [coding, docker, testing, goss]
---

# Why

During the last months I was involved in [migrating our Jenkins build infrastructure to run in Docker Containers](https://michaellihs.github.io/presentation-docker-meetup-20180215/index.html#/). One task within this process was building Docker images in which our Jenkins jobs would run. Every now and then we ran into issues that those images did not work as expected, so the question came up how we could test them.

From a more abstract perspective, your `Dockerfile` is a piece of code that can become quite complex and just like any other piece of code, you want to test it.


# Our Pipelines for Building Docker Images

Here is the workflow we use to build our Docker images:

1. start a Docker container in which we want to run the build job - all further steps run in this container
1. clone repository with `Dockerfile` and other sources to be baked into the Docker image
1. build a Docker image and tag it with a version
1. **test the images** &larr; that's what this blog post will be about
1. push Docker image to private registry


# Challenges & Requirements

Regarding the tests of the Docker images, we had the following requirements:

* builds and tests of Docker images must run in Docker containers
* we did not want to add any test-related code or binaries into the images to be built
* we wanted to test the images from "the outside"
* we wanted to test behavior (e.g. *is a http server running in the container*) as well as static configuration (e.g. *is a certain tool available in the container*)


# Introducing `goss` and `dgoss`

Since acceptance-testing an image is roughly the same as acceptance-testing any other virtualized infrastructure, immediately 2 tools came to my mind:

* [serverspec](http://serverspec.org) - which is Ruby based and normally runs from an external machine (and ssh's into the machine under test)
* [goss](https://github.com/aelsabbahy/goss) - which is a Go binary and normally runs from inside a machine

As stated under requirements, we wanted to test from the outside, so Goss did not seem like the right option at a first glance. But my dear colleague Dimitrios discovered [dgoss](https://github.com/aelsabbahy/goss/tree/master/extras/dgoss), a wrapper to Goss for testing Docker images.

The nice thing about goss is that it ships as a self-contained binary (~8 MB) and you can easily write your tests in a [yaml file](https://github.com/aelsabbahy/goss#manually-editing-goss-files). Providing a proper Ruby environment and managing dependencies has always been an issue with Serverspec, so goss sounded very promising.


# A Docker Image for building Docker Images

As mentioned above, we wanted to run the build jobs for our Docker images in Docker containers. Therefore we created an image the following way:

* extending `jenkinsci/ssh-slave`
* install docker CLI
* copy `goss` and `dgoss` to the image
* provide `Dockerfile`
* set `GOSS_FILES_STRATEGY`

Here's the `Dockerfile` that does this for us:

```
DOCKERFILE
```


# Running Goss Tests in the Build Container

Whenever we build a new image (which happens after every commit to the repository containing the `Dockerfile`) we want to run tests afterwards. So first we run `docker build ...` and then run `dgoss run <IMAGE NAME>` within the build container. As we use a [Docker outside of Docker approach](http://blog.teracy.com/2017/09/11/how-to-use-docker-in-docker-dind-and-docker-outside-of-docker-dood-for-local-ci-testing/) to provide "Docker in Docker", there are some traps that we had to workaround:

1. mount docker socket into container (`-v /var/run/docker.sock:/var/run/docker.sock`)
2. mount `/tmp` dir of host machine into the build container (`- /tmp/docker:/tmp`). This is necessary since `dgoss` running inside the build container controls the Docker engine on the host, so any mounts / copies of files into the container under test happen on the underlying host.
3. provide a `goss.yaml` file that contains the tests - this is contained in the repository with the `Dockerfile` for which we want to build a new Docker image.
4. execute `dgoss run <IMAGE NAME>` to run the tests

This results in the following command for running the

```
docker run ...
```


# Adding Goss to our Build Pipelines

## Requirements on the Jenkins Agent

* goss and dgoss installation
* temporary folder for dgoss file transfer


## Jenkins Configuration for the Agent Template

TODO add screenshot...


## Pipeline Config in `Jenkinsfile`

TODO add some code snippets


# Further References

* [goss on Github](https://github.com/aelsabbahy/goss)
* [dgoss on Github](https://github.com/aelsabbahy/goss/tree/master/extras/dgoss)
* [tutorial on how to use dgoss](https://medium.com/@aelsabbahy/tutorial-how-to-test-your-docker-image-in-half-a-second-bbd13e06a4a9)
* [Jenkins Docker Plugin](https://wiki.jenkins.io/display/JENKINS/Docker+Plugin)
* 
