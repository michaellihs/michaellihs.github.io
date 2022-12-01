---
layout: post
title:  "Meetup: Why you should avoid platform monoliths"
date:   2022-11-23 20:00:00
tags: [meetup, devops, platform, developer experience]
categories: meetup
---

These are my notes from the first "Automotive Software Development Meetup" in Stuttgart last week.

Automotive meetup
=================

On Tuesday, Nov 23rd 2022, we had our very first [Automotive Software Development Meetup](https://www.meetup.com/de-DE/automotive-software-development/) in the Thoughtworks office in Stuttgart.

For this event, we had 2 speakers, Christian Fraas from Microsoft and Michael Fait from Thoughtworks. Unfortunately I only took notes during the talk from Christian. Michael's talk was about Rust in automotive.

## Christian - Automotive Control Plane

* [Christian Fraas](https://www.linkedin.com/in/christian-fraas/)
* 1.5 years at MS, before 13 years at Daimler
* MS: "why dont we bring cloud ideas and technology in to the car"

### What is a control plane

* in the cloud
  * eg. the thing that orchestrates your network
  * does the magic in the cloud
* here: Kubernetes Control Plane
  * the thing that controls what's happening in the K8S cluster
  * "the magic that happens in the background"
  * https://kubernetes.io/docs/concepts/overview/components

### Features of K8S

* description of your deployments
* standardized API
* workload orchestration
* inventory of deployed workload
* extensible (custom resources)
* giant community and ecosystem
* ...

### Motivation

* it would be great to have all these features above to deploy software to a car
* can we bring these concepts into a car?

### In-car architecture

* there are low level ECUs (micro controller) \[majority\] in a car, mainly running on Autosar classic
* there are high-performance computers (micro processors) \[minority\] in a car, eg. head unit, telematics unit

### Automotive Control Plane

* multiple runtime technologies in a car (from low level ECUs to Docker containers)
* each of the workloads that go on such a device are deployed in a different way
  * it depends on the technology how you can update the software in the car
* this variety can lead to a big mess
  * eg. resolved by a variety of "How Tos" that explain how to flash a car
* it would be nice to have a technology-agnostic way to deploy SW to a car
  * extensible for different SW deployment technologies (eg. replace the container runtime at a later time)
  * unified configuration of different technologies
* expected capabilities
  * update
  * rollback
  * monitoring
  * delta update
* you need to be able to do that in an environment where you don't have any connectivity
  * eg. during the car being parked in a connection-less parking lot
  * crucial requirement
* Possible architecture: an update manager on top of an K3S control plane
  * reason: K8S has no dependency management for deployment procedures
* Use K3S instead of K8S to get a smaller footprint (spoiler: it's still too big)
* Interesting part: how to bring the technology in the systems that are not native K8S (custom resources vs. virtual kubelet)
  * possible solution: [virtual kubelet](https://virtual-kubelet.io/) makes a facade for the API of your target device (eg. Autosar Classic / Adaptive)
  * node (ECU) then acts like a K8S node
  * a virtual kubelet allows you to update an Autosar ECU just like a Docker container

### Eclipse Leda

* all this is "[Eclipse Leda](https://projects.eclipse.org/projects/automotive.leda)"
* allows for developers to run their application in a virtualised environment
* comes with a vehicle update manager
* self-update agent for FOTA
* collects metrics and logs and ships them back to the cloud with open telemetry

### Demo

* Leda is very basic operating system
  * Container runtime
  * DNS
  * CAN drivers
  * connectivity
  * everything is running in Docker containers
* using a virtual machine running in the cloud to emulate an ECU with QEMU
  * within this double-virtualised machine, an automotive control plane is running
* all tools that work with K8S could now "work in the car"
  * example: show all software running in a car with `k9s`
* deployment yaml looks exactly the same for in-vehicle software as for cloud deployments
* [Eclipse Velocitas](https://projects.eclipse.org/projects/automotive.velocitas) as and end2end development toolchain

### Challenges for an automotive control plane based on K3S

* resource footprint is too big for in-vehicle computers
* boot time for K3S is too long for a car
* offline update doesn't work out of the box
* self-update doesn't work out of the box
* workload distribution in a car is really static
  * K8S features for this is not required

### Questions

* how does "developer first" fits into the "embedded developer world"
  * do embedded developers really want to deal with Kubernetes?
* will the concept of embedded developers and cloud developers will merge?
  * group of developers will further differentiate
  * K8S might not be the tool a embedded developer has in mind right now
  * but anyway it will help them develop their software


### Further references

* [Software defined vehicle - Eclipse Foundation](https://sdv.eclipse.org/)
