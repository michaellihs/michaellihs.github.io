---
layout: post
title:  "Installing TYPO3 Neos in Docker"
date:   2015-04-04 21:55:29
tags: [docker, devops, continuous integration, micro services]
categories: docker
---

The goal of my "Getting Started" tutorial is to have a TYPO3 Neos installation running within Docker containers on Mac OS X. There are several tutorials and repositories available to achieve this (see Resources further down), I decided to use the [Million 12 TYPO3 Neos Docker image]. We will use the [Neos Demo Site] provided by the Neos Team as our example website. Since it is recommended to use this site package as a starting point for your own Neos projects, you not only have a "Dummy Site" at the end but a working Neos environment for your own projects.

### 1. Prerequisites

This tutorial assumes that you have [VirtualBox] installed on your machine. If not, you can [download the application here].


### 2. Download and install Boot2Docker

Download the [installation package for Boot2Docker]. This will give you a `.pkg` file that you can double-click for installation. Once the installation has finished, you have a new Application `Applications` folder called `boot2docker.app`. Double-click this app and a Terminal window (the *Boot2Docker command line*) will open up showing you the status of the boot process. Once you see something like `bash-3.2$` you are ready to go.


### 3. Launching the Docker container for the database

Following the `README` instructions from the [Million 12 TYPO3 Neos Docker image], the next step is launching a [Docker Container] for the database with which we want to run our Neos Demosite. Within the Boot2Docker command line run the following command:

{% highlight sh %}
docker run -d --name=db --env="MARIADB_PASS=my-pass" million12/mariadb
{% endhighlight %}

make sure to replace `my-pass` with the password that you want the root user of MariaDB to have (for those of you who do not know MariaDB: it is an open source clone of MySQL). If you see something like `6c46a83d.....` in your terminal window, it worked!


### 4. Launching the Docker container for TYPO3 Neos

The next step is to launch the Docker container in which the application itself - TYPO3 Neos in our case - is running. Therefore run the following command in the Boot2Docker command line:

{% highlight sh %}
docker run -d --name=neos -p=8080:80 --link=db:db --env="T3APP_VHOST_NAMES=neos.docker dev.neos.docker" million12/typo3-neos
{% endhighlight %}

Compared to the 'original command' I adapted the names for the Neos vhosts, since I have several Neos instances running in other VMs and natively on the Mac.


### 5. Creating vhost entries for the Neos vhosts

Boot2Docker creates a virtual machine and assigns an IP address to it. To find out, which IP address you got, run the following command from your Mac command line (**not from the Boot2Docker command line!**)

{% highlight sh %}
$ boot2docker ip
192.168.59.103
{% endhighlight %}

Copy this IP address and then edit your `/etc/hosts` file on your Mac to create an IP mapping for your Neos vhost. First open the file with

{% highlight sh %}
sudo nano /etc/hosts
{% endhighlight %}

then add a new line like this (where `192.168.59.103` is the IP address you determined before):

````
192.168.59.103		neos.docker dev.neos.docker
````

Quit Nano by pressing `CTRL + X` and type `Y` and `ENTER` to save the changes. Test your configuration by running `ping neos.docker`.


### 6. Working with Neos

You should now be able to open

* Neos frontend via [http://neos.docker:8080/](http://neos.docker:8080/)
* Neos backend via [http://neos.docker:8080/neos](http://neos.docker:8080/neos) with user `admin` password `password`

in a browser on your Mac.


## Next steps

For me the next steps would be to figure out, how to deploy the Neos container to another server, e.g. a Staging server or a Production server. I will cover this topic in another blog post as soon as I gathered enough knowledge to write about it.


## Further Resources

* [Seb] created a project for running TYPO3 Neos and TYPO3 Flow in Docker called [Dockerflow]
* [Boot2Docker - Install Docker on Mac OS X]
* [Docker Online Tutorial]



[Million 12 TYPO3 Neos Docker image]:                     https://github.com/million12/docker-typo3-neos
[Seb]:														http://mind-the-seb.de
[Dockerflow]:												https://github.com/Sebobo/Shel.DockerFlow/tree/boot2docker-support
[VirtualBox]:												https://www.virtualbox.org/
[download the application here]:							https://www.virtualbox.org/wiki/Downloads
[installation package for Boot2Docker]:						https://github.com/boot2docker/osx-installer/releases/latest
[Neos Demo Site]: 											http://neos-master.demo.typo3.org/
[Boot2Docker - Install Docker on Mac OS X]:                 https://docs.docker.com/installation/mac/
[Docker Container]:											https://docs.docker.com/introduction/understanding-docker/#how-does-a-container-work
[Docker Online Tutorial]: 									https://www.docker.com/tryit/
