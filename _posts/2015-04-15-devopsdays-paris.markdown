---
layout: post
title:  "One Night in Paris - DevOpsDays 2015"
summary: "For the first time me and a colleague from punkt.de attended the DevOpsDays - in Paris"
date:   2015-04-15 23:00:00
categories: devops
tags: ['devops', 'devopsdays', 'community', 'chef', 'ansible', 'docker', 'microservices']
---

The [DevOpsDays] are kind of an alternative conference covering - well - DevOps topics. There are events all over the planet - among many other inspiring places, Paris seemed like the place to go for us, since it's pretty close to Karlsruhe and you can go there by train. So here's my summary of an amazing two-days learning and sharing experience in Paris.

## Keynotes, Talks and Open Space

Every DevOps event is more or less organized in a fixed setting. There are talks in the morning and something called [Open Space] in the afternoon. For bridging the gaps between the talks and explaining things to the audience, there was a moderator guiding through the day(s).

## First Day - Talks

### Keynote - Guns, Germs and Microservices

[John Willis] started with a keynote were he draw parallels between defeating armies in ancient days and which tools led to success or defeat and the requirements in today's IT. Although I personally don't want to see myself as a developer compared to some (American / British) soldiers slaughtering other people in South America or Africa using machine guns, the point of using the appropriate tools for getting the job done was well presented. The concept of Data Gravity was well explained and it was shown that Microservices might be the right tools to tackle it.


### What happens without traction

[Steve Pereira] talked about a topic that might sound familiar to everyone who tried to establish DevOps in his or her company. He tried to show "his way" of getting other people involved in DevOps ideas by starting with himself. A good point was that one should start with observation of what is "going wrong" and then come up with solutions how to fix this in an automated way. For getting in touch with others at your company, try to find a language that resonates with the atmosphere and the culture of the company. DevOps might be a polarizing term so pick out more specific topics when talking about it: continuous integration / delivery for example or high availability, disaster recovery...

"Just because you are moving does not mean you are moving forward" - introduce the right metrics to track your progress. Use hypothesis and test them! E.g. how long does it take you (on average) to get a new feature into production. How long does it take you to recover from a certain event.

"In DevOps nothing happens without sharing" - establish an atmosphere of sharing between Devs and Ops as well as different teams in you company. As an exercise, the speaker suggested the "Product Box Exercise" - create an artificial product box for what you are working on and - together with your team mates / DevOps colleagues - fill the box with features that you want the people to advertise the product with.

Another idea was analyzing your development-operation process and try to find gaps. Therefore the speaker suggested his [DevOps Checklist].


### Why?

[Boris Feld] asked the essential question: "Why do we do DevOps?" - ans "Why do we have to ask ourselves why we do DevOps?". It turned out to be a very motivating talk on what we do and why we do it and what benefits we get from doing it.

The main statement of the talk was: DevOps is not mandatory - but

* We do it because to fail is human
* We do it because human labor is precious
* We reduce stress and waste and hence we can spend less time on boring stuff
* Automation is a good thing to beat unpredictability

Another intersting question: Why do we measure so many things (metrics, logs, ...)?

* Because we want to learn
* by collecting data, we can validate our hypotheses
* to make that what you think your customers want is what they really want
  * to be able to deliver valueable stuff to your customers
  * to make sure that a feature delivered value

A nice side note of the talk: "Company culture is what happens when the boss is not around"


### Bizdevops - from development to the customer

[Sabine Bernecker-Bendixen] was tackling the question what you have to do when you want to change something: you need to move and you got to have an open mindset. What are the challenges when working in an area of big diversity (i.e. in a Customer - Developers - Operations environment): leaving your comfort zone. Diversity is the usual setup when working in cross functional teams - so it's the common setup in DevOps environments. Following the attitude "I am ok - you are ok!" try to establish non-confronting communication. Manage your inner team when it comes to the question how to react on change. Good communication is the key to success - most of all in a mine-field like Developers and Operations working together :-)

Another aspect that I liked a lot: Start to see diversity as a resource and a value. Respect, Tolerance and the will to understand others are the most important basic values.

Love what you do and show appreciation. If you don't love the way, change it - when you change it, be respectful - be tolerant.


### How we do DevOps at BlaBlaCar

First of all - did you know [BlaBlaCar]? Well I didn't - and one day after attending their talk, we read in the news, that [they bought Mitfahrgelegenheit.de].

Within this talk, [Regis Allegre] and [Nicolas Blanc] gave an inspiring insight in how DevOps kind of developed itself in the BlaBlaCar during the history of the company. They started with only "full stack developers" so devs = ops and followed the paradigm of "Keep calm and push to production" - up to 10 times a day. After having lots of tests for production code they started to write tests for their infrastructure as well.

An interesting aspect of their team organization was that they use both, Kanban and Scrum, depending on the team's structure and purpose.

Other nice bits of their company culture is the "Thursday Beer" where employees sit together, talk about whatever they want and drink a beer (talking with each other in such a setting makes it much easier to work together later on and tackling "complicated" issues) - and the "Weekly Free Speech", where the subject is chosen by vote (e.g. Docker, Varnish, Packaging, ...).

Their conclusion: DevOps culture is mainly communication.


## First Day - Open Space

In the afternoon, Open Space sessions took place. After an introduction to the technique itself, every attendee was invited to hand in a topic he or she wants to talk about. The topics were then collected on a board and dot voting was used to select the topics that actually became sessions. There was space for 3 slots in 4 parallel tracks. Before the sessions started, 4 rules were given by the organizers:

1. Whoever comes [into your session] - it's the right people
2. Wherever it [your session] happens - it's the right place
3. When it [your session] is over, it's over
4. We can't change the past, we are not in the future, it's important what happens right now

Besides, there was the "two feet law" which means: whenever you don't like the session or heard enough, just move on (to another session).

### Slot 1: Docker 101

[John Willis] showed the first steps with Docker in an add-hoc session. You can more or less have the session on your own, by following his [Videos from the Docker Blog] and his [Docker Cheat Sheet].


### Slot 2: How to make test automation robust

Someone from IBM introduced "their" way of doing automated frontend testing with [Selenium] and a self-written framework on top of it. The framework enables testers to write their tests with a very simple subset of the Java language without having to know any details about Selenium.

During the discussion, others mentioned the [Gherkin] language for writing tests and implementations in PHP ([Behat]) and Ruby ([Cucumber]) as well as the concept of [Behaviour Driven Development (BDD)].

A discussion started about the right usage of Unit Tests compared to Integration Tests and Acceptance / UI Tests. The participants agreed, that the [Testing Pyramid] should look more like a testing square.


### Slot 3: Microservices

For me the session where I learned most, was this slot. Maybe because I'm completely new to this topic or maybe because of the people in the session and that [Microservices] are a rather new technology - it was simply inspiring.

We talked about how to split monolithic legacy applications into Microservices. Where to start? One way is to use a (well encapsulated?) part of the application, wrap it in a service and maybe implement it in a new programming language that fits better for the kind of application than the language of the legacy application.

Other aspects were how using Microservices can cause organizational change as much as it causes system changes.

I was made aware of that just by putting services in self-contained containers does not necessarily make things easier, but maybe complexity is shifted from inside the containers to orchastrating them and keeping things up and running, scaling and distributing stuff and finally doing backup etc.

Another hard problem to implement Microservices is transactions and referential integrity across multiple services.


## First Day - Evening Event

The evening event took place in an old theatre in the center of Paris - actually it was within a few minutes walk of the city hall and Notre Dame. Drinks and food were free and it had just the right size to get in contact with many people. As an attraction you got 500€ gamble money at the entrance and could play Blackjack and Roulette.

We left the theatre around 10 at night and took the chance to walk through Paris - visiting Tour Eiffel and walking back to our hotel.


## Second Day - Talks

### Cognitive biases and our poor intuitions around probability

In his brilliant keynote for day 2, [Nigel Kersten] talked about cognitive biases. What are cognitive biases? Errors in how we process and interpret information, mainly due to heuristics that simplify information processing. The speaker mentioned two "systems" that kind of run in our brain in parallel: System 1 - responsible for fast decisions, and System 2 for long running decision making, taking into account lot more aspects than system 1.

It was further shown that we are not very good when it comes to probability and that this is something we even stumble upon as adults. As one example where probability tricks people the law of large numbers was presented. In the examples of the talk, this broke down to seeing patterns in random data, e.g. connecting "random" failures with unconnected entries in log files in computer systems. According to the speaker this happens especially if you put people under stress or if they think that things are not under their control (any more). In order to prevent this situation: prevent stress and give the people the impression that they have things under control.

Another hypothesis of the talk: we are bad at estimation. It gets much better, once when we have data to rely on.

For the communication in our companies, Nigel mentioned another interesting effect:

* Ask people for 6 occasions when being assertive
  * They will think they are assertive
* Ask people for 12 occasions
  * Given they have to think about this for a longer time and probably don't come up with as many as 12, they think they are not assertive

The interesting part is that you can actually negate this: Ask people for 12 ocassions when they were not assertive and they will think they are assertive. The rule behind this is that we are less confident in a choice, when we have to come up with more arguments for it.

As an important rule for our daily work: don't blame people in post-mortems! Don't ask for everything that could've been done to avoid something.

Some further advice:

* Use frequencies instead of probabilities
* Think diagrammatically (Venn diagrams...)
* Internalize that we think that random data contains patterns

Relieve System 2 (it gets tired very fast)

* Make important decisions early in the day
* Minimize unimportant decisions

[slides](https://speakerdeck.com/nigelkersten/cognitive-biases-and-our-poor-intuitions-around-probability)


### Designing the Enterprise for Manufacturing

[Scott Russell] talked about the transition from "traditional" manufacturing processes to a software manufacturing process. As a provocative statement, he mentioned that if you are doing something complex in manufacturing, you are probably doing it wrong.

There is an interesting parallelism between assembly lines in classic industries and production lines in IT. Scott presented two types of such lines: a Jobbing Shop - with plenty of handwork and no straight order of production steps and continuous flow. The first one is very likely to have bottlenecks and uncontrolled queuing and we don't want to work in such a manner in IT. The straight continuous production line enables us to work in small batches.

Another term we know from industrial production is changeover time. This can also be mapped to IT industries. Think about how long it takes you as a developer to switch from one project to another or to switch from one product variant to another.

Move from Quality control to Quality assurance and from quality inspectors to quality trainers. Don't spend time on checking every item but use a significant sample instead. Use the time saved to train your people in sense of how to prevent the quality issues you discovered. This can directly be transferred to a peer-review based quality assurance, e.g. with code review.


### Change management at scale: responsible agile delivery

[Pierre-Yves Ritschard] talked about tools for change management. Unfortunately I was not able to get all the information in his talk so that I could present it here in a compact way. He mentioned a "tool" called [ITIL - Information Technology Infrastructure Library] as a set of best practices for change management in organizations and mapped some of this tooling to tools we know from the DevOps world.

He recommended avoiding blocking management instruments like meetings or boards when it comes to changes and rather rely on peer review and auto-validated change mechanisms.

A interesting tool he mentioned is [WARP](https://github.com/pyr/warp).


### Making the Elephant dance – Daily deliveries at SAP

[Dirk Lehmann] gave an insight to his work at SAP and how his team achieved to come up with the first SAP product that is delivered on a daily basis. He described the "rest of the SAP software" as hard to be delivered continuously and showed how his team became kind of a early adopter for continuous delivery in their company.

Since many talks at DevOpsDays covered the topic of how rolling out DevOps in larger organizations can be a stony path, this was maybe a real world instance of this problem.


### Screwing up for fun and profit

[Oliver Hankeln] talked about managing failure and what we can learn from mistakes. He started with the definition of what a mistake is, namely a decision or judgement that led to a negative outcome, which could have been prevented given the resources and knowledge at time.

Further on, Oliver talked about effective learning and what's necessary for it: Transparency, searching (and finding) the root cause, trust (in your colleagues) - what they say is the truth, what you say won't be used against you in a later time - and Respect.

He then talked about a method called *Post Mortem* which originates in medicine where you want to find out, why a someone died.

Here's how it works

* bring together people from all effected departments
* collect timeline of events (events can be added any time during the meeting)
* try to find the root cause
  * not "this person was tired" - but "why was this person tired"
* define actions afterwards
  * who does it
  * when will it happen

Together with this method, Oliver presented a set of (Anti-)Patterns how to conduct a post mortem.

**Anti-Patterns for coping with mistakes**

* Hiding Mistakes
	* CEO Disease: the higher you get, the more people only talk about successes, not failures
	  * CEO has no clue what's going on in his company
	* Wasted learning opportunity
	  * if you don't talk about failures, how can others learn from them
	* financial bonus often leads to hiding mistakes
	  * incentive based on uptime might prevent you from making change
* Blame Game
	* Blame leads to reaction
	  * blamed people start to defend themselves
	  * aggression and fear disable learning
	  * root cause gets hidden
	* blamed people are not willing to help
* Arc of Escalation (going to your boss to complain)
	* You play Chinese Whispers (stille Post)
	* You force a blame game
	  * Once the boss is there, the other guy feels blamed for sure
	* you destroy trust
* Cowardice
	* Time wasted on formalities
	  * Everything you do, you need permission of someone
	* No one want to be responsible
	* Cause: punishing or firing people who screw up

**Patterns for coping with mistakes**

* Proactive communication <--> Hiding Mistakes
  * Be open about the failure
  * Now have a post mortem
  * Talk about what was learned
* Accepting <--> Blame Game
  * Post Mortem is NOT a performance review
  * Focus on events not on (groups of) people
  * Prime Directive
* Talk to your peers <--> Arc of Escalation
  * Be aware of confirmation bias
  * "They are nice guys!"
  * Try to switch perspectives
    * Try to see things through their eyes
* Embrace Failure <--> Cowardice
  * You are a ninja!
  * You are a scientist - whatever you do, it can fail!
    * Failures help us to learn
    * Learning adds value to the company
  * You are an adventurer
    * Accidently, you can stumple about something great, new

Oliver pointed out that it's hard - if not impossible - to Predict failure. What you can do instead is a method called *Pre Mortem*. There fore you do the following:

* Gather people from different departments
* Start with a catastrophic outcome and try to analyze why it happenedd
  * Use it as a brainstorming session about what might have happened that lead to the described catastrophe
  * be playful and have fun
* Repeat the game with different groups

Conclusion: A mistake is only a failure if you don't learn from it

## Day Two - Ignite Session

Ignites are 5 minutes presentations where the slides run automatically in the background while someone presents a topic. There had been two memorable presentations on the second day. I missed the first day's ignites, since we went for a run...

### Ignite - Automating Jenkins

* UI of Jenkins is not really user-friendly when it comes to bulk-updates
* Use puppet manifests to automate Jenkins
* All projects are build exactly the same way
* Configurations are versioned

### Ignite - Git deliver

* Tool for running deployments with git
* Provides a new git command `git deliver <remote> <version>`
* Provides rollback
* Deployments are atomic
* Deliveries are organized in stages - you can hook in every stage
    * hooks can be shared across projects / people
* see [http://github.com/arnoo/git-deliver](http://github.com/arnoo/git-deliver)


## Day Two - Open Space

### Open Space Slot 1: Automating Jenkins

* Using Groovey for automating Jenkins / writing Jenkins Jobs
  * Transformation of Groovey to XML that is then imported in Jenkins
* Use Jenkins API to load the (new) configuration
* Good idea: All projects are build in the same way
  * Keep the configuration outside of the projects
  * Have shell scripts inside the projects that hold the steps that are actually run in the Jenkins jobs
  * Projects knows "what to run"
  * Configuration knows "how to run"
* JenkinsJobBuilder (OpenStack Tool?) http://ci.openstack.org/jenkins-job-builder/
* Bottlenecks and scalability of Jenkins installations
  * Master / Slave scenarios scale very well
  * Master is only there to orchestrate
  * No jobs on the master!
* There seems to be no easy to adopt solution for feature branches
  * Recommendation: trunk-based development
  * Parametrized build jobs that take branch name as parameter


Open Space Slot 2: Deployment of Microservices
----------------------------------------------

* First of all: Microservices have nothing directly got to do with Docker
  * Microservices is an architectural approach
  * Docker is a platform to run them
  * Microservices can run on many other platforms
    * This can be an isolated environment (e.g. like Docker Containers)
    * or a system with many other services on it
* Complexity moves from monolithic application to orchestrating many small services
* Problems might occur, when you have to run services in (probably many) different versions
* Do not use database integration
  * Build a bounded API around an encapsulated domain
  * Handle data access through APIs
* Microservices themselves do not solve issues with handling schema changes in databases
* Use 12-factor app principles to design and build microservices


Open Space Slot 3: Organizational Structures for DevOps
-------------------------------------------------------

* Problem with specialization
  * There is specialization amongst Devs (Frontend, Backend, Languages) as well as amongst Ops (Networking, Backup, Firewall...)
  * Share knowledge
  * Distribute Ops in Dev Teams to create independent teams
* Teams supporting teams, to make them more autonomous
  * Deliver services, so that other teams become more independent
* Ops write recipes helped by experts
  * Use code review "from both sides"
    * Ops check whether recipes written by Devs do what they should do
    * Devs check whether recipes need to be refactored


## Summary

DevOpsDays Paris was a great experience - starting with the location, the food, the people and of course the inspiring talks and sessions. I can definitely recommend going there. Given the fact that this is a non-profit event and the fees are comparably low (at least when compared to other conferences) - this is a must-go for all people interested in DevOps. The topics  made a really nice mix of rather abstract stuff in the talks and more technical things in the sessions in the afternoon.

Thanks a lot to all the people that made this event possible and the sponsors!



[DevOpsDays]: http://www.devopsdays.org/
[organizing guide]: http://www.devopsdays.org/pages/organizing/
[Open Space]: http://en.wikipedia.org/wiki/Open_Space_Technology
[John Willis]: https://twitter.com/botchagalupe
[Steve Pereira]: https://twitter.com/steveElsewhere
[Boris Feld]: https://twitter.com/lothiraldan
[DevOps Checklist]: http://devopschecklist.com/
[Sabine Bernecker-Bendixen]: https://twitter.com/SabineBendixen
[they bought Mitfahrgelegenheit.de]: http://www.deutsche-startups.de/2015/04/15/blablacar-uebernimmt-mitfahrgelegenheit-de/
[BlaBlaCar]: https://www.blablacar.de/
[Regis Allegre]: https://twitter.com/metalmumu
[Nicolas Blanc]: https://twitter.com/thewhitegeek
[Videos from the Docker Blog]: https://blog.docker.com/2015/03/docker-tutorial-1-installing-docker/
[Docker Cheat Sheet]: https://gist.github.com/botchagalupe/53695f50eebbd3eaa9aa
[Selenium]: http://www.seleniumhq.org/
[Gherkin]: https://github.com/cucumber/cucumber/wiki/Gherkin
[Behat]: http://docs.behat.org/en/v2.5/
[Cucumber]: https://cukes.info/
[Behaviour Driven Development (BDD)]: http://en.wikipedia.org/wiki/Behavior-driven_development
[Testing Pyramid]: http://martinfowler.com/bliki/TestPyramid.html
[Microservices]: http://shop.oreilly.com/product/0636920033158.do
[Nigel Kersten]: https://twitter.com/nigelkersten
[Scott Russell]: https://twitter.com/sc0ttruss
[Pierre-Yves Ritschard]: https://twitter.com/pyr
[Dirk Lehmann]: https://twitter.com/doergn
[Oliver Hankeln]: https://twitter.com/mydalon
[ITIL - Information Technology Infrastructure Library]: https://www.axelos.com/best-practice-solutions/itil/what-is-itil