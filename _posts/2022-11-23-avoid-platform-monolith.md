---
layout: post
title:  "Meetup: Why you should avoid platform monoliths"
date:   2022-11-23 20:00:00
tags: [meetup, devops, platform, developer experience]
categories: meetup
---

These are my notes from the [Thoughtworks meetup on Nov 23rd 2022](https://www.meetup.com/de-DE/ThoughtWorks-Muenchen/events/289371760/) with [Marion Bruns](https://www.linkedin.com/in/marion-bruns-673282/) and [Rahul Punjabi](https://www.linkedin.com/in/punjabirahul/) about platform monoliths and why you should avoid them.

Why you should avoid platform monoliths
=======================================

Some background
---------------

* platform as enabler for enterprises to deliver customer value quickly
  * in this talk, focus on developer platform

* why invest? 
  * t2market, cost efficiency, reliabilit, security

* reality check for dev platforms ("have you faced these challenges?")
  * become bottlenecks
  * low adoption
  * insufficient performance
  * new features take long time
  * costs are rising

> online poll reveals: "some of them apply to 57% of the audience"

Why do platforms fail?
----------------------

* treating cloud like on-prem DCs 
  * delegated to team that previously maintained on prem DC
  * ticket based
  * silos
  * no interaction with outer world
  * no prod thinking
  * "it takes more to enable autonomous teams and the business value you want to achieve"
* not planning for right scale
  * scaling up AND scaling down (starting with tons of resources, not really required)
* assuming what platform customers want
  * "we wil build something and they will come" -> does not really happen
  * lack of collaboration with future customers
  * lack of product thinking
* unbalanced capabilities across teams
  * things get developed in isolation
  * when times come, devs need to be onboarded without proper capabilities
  * platform tends to be too complex

Traditional drivers: monolithic platform formula 
------------------------------------------------

> seen by a lot of clients, when first approaching TW)

* what do we mean by that?
  * "platform team box in the cloud"
    * users and access key, IAM, CI/CD, networking, logging, monitoring
    * compute orchestrator (K8S or EC2 instances)
    * "if you want DevOps, Jenkins is probably the first step"
    * underlaying: runtime cluster of nodes
    * service mesh in the middle between cluster and customer workload... service discovery, circuit breaking, service2service comm...
    * client workload running on top, eventually "soft" isolation of workloads
  * issue with service mesh - ask: do you really need that? only makes sense with micro services at scale
    * often get implemented without actual need, very complex
    * service meshes can slow down entire architecture
  * last but not least: data as the most sensitive asset of your company
    * data is part of the "platform box" - data is sitting there... customer data, product data, potentially highly confidential
    * sits in the same box that is accessible by everybody
* there are some use cases where this box-approach can work
  * but many times, this approach does not work
* centralized platform IS NOT a sensible default
  * security
  * reliability
  * maintainability
  * performance

Why is the this monolithic platform formula NOT a sensible default
------------------------------------------------------------------

* security incidents
  * ask: "when and how they might happen" not "if they may happen"
  * think about the attack surface, how might an attacker attack the platform
  * what permissions do your roles allow?
  * how and where is your data stored - how granular are permissions to data...

* share multi-purpose platform
  * one container orchestrator vs. workloads of varying characteristics that should run on the platform
    * example: one CI/CD system for all customers, but runners might have completely different characteristics in terms of platform requirements
  * capacity management
    * despite automated measures in the container orchestrators, you will be flooded with requests for fixing resource issues
  * you lose the capabilities of modern cloud in terms of scalability...

* Cluster administration with an enormous failure radius
  * how much effort do you have to put into patching and upgrading
  * what about the likelihood that an individual workload can block your cluster from udpating appropriately
  * what about your confidence in recovering from cluster-wider failures?

* Multi-tenancy limitations
  * maintaining multi-tenancy on compute, storage and network is complex
  * there are a lot of measures that can be taken & provided by cloud provider, but implementing them can become very tedious
  * you easily run into an amount of policies that are hard to maintain on a platform level
  * limitations in network resources (IPv4 addresses, ports...)

What are the solutions at hand? 
-------------------------------

> What can we learn from Microservices, Data Mesh & Evolutionary Architecture (applied to developer platforms)

* Architectural Quantum
  * independently deployable component with high functional cohesion, required by system to function properly

Formula for the design of a decentralized platform
--------------------------------------------------

* Dedicated architectural quantum for each customer
  * Azure: one subscription for each customer
* what's inside
  * compute
  * network integration
  * observability tooling
  * ...
  * IMPORTANT: capabilities depend on your use case
* how is this benefitial
  * security incident: fix it for one affected customer
  * setup auto-scaling suitable for the one workload / use case of customer
  * you won't run out of resources for an individual customer (as long as cloud provider can offer more)
  * you can apply horizontal scaling (if needed)
* shared services in platform
  * hybrid networking
  * inter-quantum networking
  * internet connectivity
  * DNS and service discovery
  * compliance automation (making sure, users follows policies)
* platform services (will vary from context to context - this is just a spectrum)
  * IaC and pipelines for infrastructure management
  * compliance and government policies
  * developer portal
  * community forum
* we encourage to put as many capabilities as possible in the quantum, since it is still managed by the platform team
  
* Outcomes of running decentralized platforms at scale
  * applied to multiple public cloud providers - approach worked for multiple clouds
  * how long does it take: productive customers within the year of inception
  * allows for self-service for the teams
  * allows for security guard rails
  * increased cost-transparency

Core capabilities and practices for successful platform strategies
------------------------------------------------------------------

* it's more than just implementation - eg. balance capabilities across teams - how do I approach in a way that everyone can benefit from it

* Product Thinking
  * do user research, get requirements from your customers, do enough research to get those requirements
  * Define measures of success - you have to do this right from the start - are you helping your customers or are you getting in their way?
  * product strategy - product owner who can aling with business objectives - have a platform to serve the business objectives
  * establish and communicate service level objectives

* shared responsibility
  * mapping technical capabilities and interfaces (interfaces in terms of "how do you collaborate")
  * what does it mean to define technical capabilities
    * define collboratively the needed tech capabilities
    * define model on how you offer capabilities (just documentation, code snippets, ...)
    * define the interaction model with the development teams (self-service, developer portal, ...) - but even close collaboration with the dev team
    * how do you want to onboard? you might even need to go into the team(s) and help them with onboarding

* self-service
  * invest in a developer portal (eg. Backstage)
    * step-by-step guide in how developers can make use of services
    * there should be no need for devs to write tickets to get something (onboarding new user, new VM...)
  * build automated, dev friendly interfaces
  * provide paved paths for frequent user journeys
  * build in quality gates and guardrails

* Lightweight governance
  * enable autonomous teams!
  * treat principles and guardrails as living artifacts
  * use compliance as code and automation to enforce them
  * continuously collaboration on those principles - allow for users to work and aling on these principles - collaboration is key

Some of the challenges
----------------------

* Isn't this more expensive?
  * return question: how are you looking at costs?
  * consider hollistic view of costs over local optimization
  * when slowing down customers with monolithic platform eg., experimentation, platform reduces competitive advantages of your dev teams

* Orchestration of dependencies across platform infrastructure

* Balancing infra capabilities across platform and customer teams (especially when starting with the platform)

Takeaways
---------

* monolithic platforms can restrict its own evolution and restric the customers
