---
layout: post
title:  "DevOps Meetup Stuttgart: Automated Security Testing in Continuous Integration"
date:   2020-03-05 21:55:29
tags: [meetup, devops, continuous integration, security]
categories: continuous integration
---

This is a short summary of our [DevOps Stuttgart Meetup from March 5th](https://www.meetup.com/de-DE/devops-stuttgart/events/268094799/) about automated security testing in Continuous Integration. For the meetup we had [Christian Kühn](https://twitter.com/CYxChris) and [Arnold Franke](https://twitter.com/indyarni) from [Synyx](https://synyx.de/) with us as speakers.

Chris started the presentation with a question who is currently running security tests in their pipelines and I was surprised by the majority of hands being raised. Also it seems like nowadays more then half of the audience is running production workloads in containers.

For motivating the topic of security testing, we've been introduced to a recent [security incident at Euquifax](https://www.synopsys.com/blogs/software-security/equifax-apache-struts-vulnerability-cve-2017-5638/), where a huge amount of private data (i.e. social security numbers and credit card data) leaked, due to a non-patched Java library. The point is that this incident could have been avoided with proper scanning of dependencies and timely patching.

Afterwards the presentation mainly covered the following topics:

* How security is treated in many software projects, a.k.a. "I am a developer, leave me alone with your security stuff, we have a team / specialists for that"
* Short introduction to [OWASP Top 10](https://owasp.org/www-project-top-ten/) and the [CVE database](https://nvd.nist.gov/vuln/full-listing) from NIST
  * TOP 9 is *Using Components with known vulnerabilities* which we took a closer look at
* **Dependency scanning** with a ["broken" Spring Boot](https://github.com/cy4n/broken) app as an example
  * showing that even the simplest Spring Boot application has > 50 transitive dependencies
  * so a first important learning of the evening was do not only take care of the code you write, but **know your dependencies**
* Introduce **security scans in pipelines** - with an example of how this can look like in Jenkins
  * distinguish between broken builds and **unstable builds**. Reason for this is to still be able to ship your artifacts with having vulnerable dependencies in them - as long as you work around the issue within your code.
  * **Whitelisting depenendencies** in dependency security scans allows you to mute findings in your dependencies if they do not impact your artifact (e.g. vulnerabilities in a library that only impact your application when you use a certain feature)  
  * presented **tool for security scans** was [OWASP Dependency Check](https://owasp.org/www-project-dependency-check/)
  * other tools of interest might be [snyk](https://snyk.io/), GitHub offers [security scanning for free](https://help.github.com/en/github/managing-security-vulnerabilities/about-security-alerts-for-vulnerable-dependencies) on open source projects
* What are the security-related issues with using Docker images
  * Docker images are often based on other images, hard to track versions, if using `:latest`
  * base images are maintained by the community and are usually patched properly
  * custom intermediate images are often problematic since people tend to forget about them
  * widely used anti-pattern: we have nightly builds of our software and application images but forget to patch intermediate images
* **Container Scanning** - scans Docker images for known vulnerabilities
  * presented **tool for container / image scanning** [CoreOS Clair](https://github.com/quay/clair)
  * there is a Docker image to run clair on demand [clair-local-scan](https://github.com/arminc/clair-local-scan)
  * it is challenging to figure out, which vulnerabilities are critical for you
  * there is **another tool for scanning images** [trivy](https://github.com/aquasecurity/trivy)
  * hint: run tests in multiple vulnerability testing tools and check which findings are relevant for you
* scan your applications endpoints in an **API Scanner**
  * presented tool for automated penetration tests for APIs is [OWASP ZAP](https://owasp.org/www-project-zap/)
  * how it works is that a spider first of all generates a list of endpoints for your API that is then passed on to a penetration test
  * you can also feed your **Open API definition** in a [Swagger](https://swagger.io/specification/) format to make the tool aware of your actual endpoints
  * by looking at the tests ZAP is running against your app **you can already learn a lot about application security**
  
So in summary, we learned how to add 3 new stages to our Build Pipeline which are

1. Security checking of dependencies
2. Vulnerability scanning for Docker images
3. Penetration testing your (REST) API in the running application

and about the challenges with properly using the three tools and their findings. 

After the presentation, someone mentioned [OWASP Secure Codebox](https://owasp.org/www-project-securecodebox/#) as another tool you might want to take a look at.

The lively discussion after the presentation showed that it was very well received by the audience. We hope to have further security topics in our [DevOps Stuttgart Meetup](https://www.meetup.com/de-DE/devops-stuttgart/) in the near future. If you want to give a talk, feel free to reach out to me any time.

Here's the [link to the slides](https://www.slideshare.net/ChristianKhn8/automated-security-testing-in-continuous-integration).

A big Thank You! goes to the team at [ZOI](https://www.zoi.de/) and especially [Malte](https://twitter.com/derBroBro) who provided a pleasant location and food and drinks.
