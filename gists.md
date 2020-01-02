---
layout: page
title: Gists
permalink: /gists/
---

Github Gists and Cheat Sheets
=============================

This is a list of Github Gists that I use to remember noteworthy stuff... feel free to fork and extend!

* [Pacman in Golang](https://gist.github.com/7afdd9a8088e893b84be3046bafb8807)
* [Container Security](https://gist.github.com/fcd4453e309b986c9076851657175f1f)
* [jsonnet](https://gist.github.com/09ed1a4c527a54c1a5f010b95579b6ee)
* [Gradle OSS Dependencies](https://gist.github.com/937e5bd28ac231c1038a356d822342d5)
* [Molecule Learnings](https://gist.github.com/c29baff6ec6640cc4c210a55dc7f7afe)
* [Outside-In TDD](https://gist.github.com/541927e083dcaa78532a8f6fef9bd280)
* [BUCC on GCP](https://gist.github.com/c2c0bd258610904514e7301474a2dc8f)
* [Jenkins is dead - long live Jenkins!](https://gist.github.com/b24c78071b34decc5fe79fd01a51f7f2)
* [Google Cloud Platform](https://gist.github.com/084062ef7baf65f1b19d252a0078937e)
* [Kubernetes the Hard Way](https://gist.github.com/c213ded09dd5cd84bf87352782bca001)
* [SSH with Vault](https://gist.github.com/32d2abb0be0e2936654d7d169133a94f)
* [Jenkins CLI](https://gist.github.com/e1b038084d14d577b9ecd49f8e332ffb)
* [Vagrantfile with Proxy config](https://gist.github.com/f4bc4f297d696f7186448f7198f24b06)
* [DevOps Principles](https://gist.github.com/3177c39a5b9b9c1012ea9ba9aee686b3)
* [Get Jenkins Plugin licenses](https://gist.github.com/a844a93cb3575beb2693807435f27649)
* [git resources](https://gist.github.com/7bbaef6b4f4731452e6b0801cca17625)
* [Docker Cheat Sheet](https://gist.github.com/de0116a38b8f0b3707581b827ea536d6)
* [Ansible Cheat Sheet](https://gist.github.com/dce661376674692f0e8a5694ece2ffb6)
* [Meetups](https://gist.github.com/3e598bfa3172853f6019eb6340c0c649)
* [Go Cheat Sheet](https://gist.github.com/4e35ed9546f379a3ef0583644d760bce)
* [Consumer Driven Contracts](https://gist.github.com/e302a4a8450ca28cbd51f56968157e45)
* [Create Gitlab Personal Access Token using curl](https://gist.github.com/5ef5e8dbf48e63e2172a573f7b32c638)
* [Docker Cheat Sheet](https://gist.github.com/9130d1db63ea973b9f1b0572b6d3aca2)
* [Upload tracks to Strava from the Command Line](https://gist.github.com/bb262e2c6ee93093485361de282c242d)
* [Fenced code in bullet lists with GitHub-flavoured MarkDown??](https://gist.github.com/3689b0a246d8bfb43176fa32633eb59d)
* [Setting Maven artifact in pom.xml with command line tool ](https://gist.github.com/bd7c540870353fea13000dc37acab361)
* [Semantic Versioning class for Groovy](https://gist.github.com/a6621376393821d6d206ccfc8dbf86ec)
* [Groovy script that returns an array of Git tags with versions](https://gist.github.com/bd13d7f7d966d2ccf7ab57bc651c1d12)
* [bash / shell cheatsheet](https://gist.github.com/43a506058d6d998e02f305b7332915bc)
* [Go CheatSheet](https://gist.github.com/0648fddec0ae2f61bb877732b33679a0)
* [Summary of cfgmgmtcamp 2017](https://gist.github.com/b6c38898ad8a98dcd7c183238592166c)
* [Networking Cheatsheet](https://gist.github.com/28d999184c0939449463735b7fc10307)
* [Networking Cheat Sheet](https://gist.github.com/8273c3258baa008dbbce68686a667e27)
* [BOSH Cheat Sheet](https://gist.github.com/afdcfbe0b5f46c6bfacacd0ec1322ba0)
* [Concourse Cheat Sheet](https://gist.github.com/f3bdf918a46c2d82bc05ce2d5a9a8fea)
* [Resources for BOSH](https://gist.github.com/09c52a84318ad3b73f6c82da3633ab7d)
* [Spring Boot Testing](https://gist.github.com/3dcaaf3cf6cbbf18f88728ec78dc7230)
* [Spring Bean Injection](https://gist.github.com/700cb3bfd961e1566682040fce6d4e98)
* [tmux Cheat Sheet](https://gist.github.com/b6d46fa460fa5e429ea7ee5ff8794b96)
* [Git Cheat Sheet](https://gist.github.com/ec20000de92980d122785d5b28a3ec78)
* [Mac OS Cheat Sheet](https://gist.github.com/4ace21f2d913ef989109e07304b904cd)
* [Swagger Cheatsheet](https://gist.github.com/31112346a6c65be0e4379756d0652108)
* [Jenkins Pipeline Plugin Cheat Sheet](https://gist.github.com/6574ca201ad951d28182e63a35b8a269)
* [Maven Cheatsheet](https://gist.github.com/b08c89581ec597fa198cf74e2239f4a6)
* [Some Snippets and Resources for BOSH](https://gist.github.com/e205063847e853e87a7d9c1b4bf7aaa9)
* [Opens a Gitlab site for the current directory](https://gist.github.com/eb65d4f32cb203764ad9)
* [Write your own ssh Server with the Python Twisted library](https://gist.github.com/d2070d7a6d3bb65be18c)

> Note to myself: here is the command that gives me all my gists as JSON
> 
> ```bash
> curl 'https://api.github.com/users/michaellihs/gists?per_page=100' | jq '[ .[] | {url: .url, description: .description}]'
> ```
>
> and here is the VS Code replace regex to format them into Markdown
>
> ```
> \{\n.*(https.*?)".*\n.*"(.*)"\n\},
> * [$2]($1)
> ```