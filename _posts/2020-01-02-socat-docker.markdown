---
layout: post
title:  "Socat and Docker"
summary: "How to monitor Docker network traffic with socat"
date:   2020-01-02 20:00:00
categories: docker
tags: [docker, linux]
---

Recently, I learned how to use [socat](https://linux.die.net/man/1/socat) to monitor the network traffic between the Docker CLI and the Docker host. This works by proxying the communication via socat and sending all traffic to stdout. Here is how it works for either Unix sockets or TCP sockets.


Installing `socat` on Mac
-------------------------

If you are running on a Mac, you first need to install `socat` - easiest done via Homebrew

```bash
brew install socat
```


Monitoring traffic with Unix socket
-------------------------------------

> assuming we have the Docker daemon listening on a Unix socket `/var/run/docker.sock`

Open a first terminal and run

```bash
socat -v UNIX-LISTEN:/tmp/docker.sock,fork UNIX-CONNECT:/var/run/docker.sock
```

now open a second terminal and run

```bash
docker -H unix:///tmp/docker.sock ps -a
```

You will see all HTTP traffic between the Docker CLI and the daemon in the first terminal.


Monitoring traffic using TCP socket
-----------------------------------

> assuming we have the Docker daemon listening on a TCP socket `127.0.0.1:1234`
>
> if you don't have the Docker daemon listening to a TCP socket, you can first "simulate" this via
>
> ```bash
> docker run -d -v /var/run/docker.sock:/var/run/docker.sock \
>     -p 127.0.0.1:1234:1234 \
>     bobrik/socat TCP-LISTEN:1234,fork UNIX-CONNECT:/var/run/docker.sock
> ```
>
> this will make the Docker daemon listen on `127.0.0.1:1234`

Open a first terminal and run

```bash
socat -d -d -v TCP-LISTEN:2345 TCP4:127.0.0.1:1234
```

now open a second terminal and run

```bash
docker -H 127.0.0.1:2345 ps -a
```

Again, you will see all traffic between the Docker CLI and the Docker daemon in the first terminal.



Further References
------------------

* [socat man page](https://linux.die.net/man/1/socat)
* [great blog post on socat by Cindy Sridharan](https://medium.com/@copyconstruct/socat-29453e9fc8a6)
