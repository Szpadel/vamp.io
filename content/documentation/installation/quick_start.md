---
title: Quick start Marathon
type: documentation
weight: 40
aliases:
  - /quick-start/
  - /getting-started/
menu:
    main:
      parent: installation
    
---

# Quick start with Marathon

The easiest way to get started with Vamp is by spinning up one of the Docker images stored
in the [vamp-docker repo](https://github.com/magneticio/vamp-docker) and the [public Docker hub](https://hub.docker.com/r/magneticio/vamp-docker/).
This setup will run [Marathon](https://mesosphere.github.io/marathon/) and Vamp inside a Docker container with Vamp's Marathon driver.

## Step 1: Get Docker

Please install one of the following for your platform/architecture

- Docker 1.9.x (Linux), OR
- [Docker Toolbox 1.9.x] (https://github.com/docker/toolbox/releases) if on Mac OS X 10.8+ or Windows 7+

> **Note:** Running Vamp Quick Start on Docker 1.10.x requires a small change and we will provide the new Docker image soon.  

## Step 2: Run Vamp

Start the `magneticio/vamp-docker:0.8.3-marathon` container, taking care to pass in the right parameters. 

### Linux

A typical command would be:
{{% copyable %}}
```
docker run --net=host \
           -v /var/run/docker.sock:/var/run/docker.sock \
           -v $(which docker):/bin/docker \
           -v "/sys/fs/cgroup:/sys/fs/cgroup" \
           -e "DOCKER_HOST_IP=`hostname -i | awk '{print $1;}'`" \
           magneticio/vamp-docker:0.8.3-marathon
```
{{% /copyable %}}

Mounting volumes is important. 
Great article about starting Docker containers from/within another Docker container can be found [here](https://jpetazzo.github.io/2015/09/03/do-not-use-docker-in-docker-for-ci/).

> **Note:** Marathon port is 9090 (e.g. http://localhost:9090/) instead of default 8080. 


### Mac OS X 10.8+ or Windows 7+

A typical command on Mac OS X running Docker Toolbox would be:
{{% copyable %}}
```
docker run --net=host \
           -v /var/run/docker.sock:/var/run/docker.sock \
           -v $(which docker):/bin/docker \
           -v "/sys/fs/cgroup:/sys/fs/cgroup" \
           -e "DOCKER_HOST_IP=`docker-machine ip default`" \
           magneticio/vamp-docker:0.8.3-marathon
```
{{% /copyable %}}

> **Note:** If you installed Docker Toolbox please use "Docker Quickstart Terminal". At this moment we don't support Kitematic yet.

After some downloading and booting, your Docker log should say something like:

```
...Bound to /0.0.0.0:8080
```

Now check if Vamp is home on `http://{docker-machine ip default}:8080/` and proceed to our [getting started tutorial](/documentation/guides/)

![](/img/screenshots/vamp_ui_home.gif)

Exposed services:

- HAProxy statistics [http://localhost:1988](http://localhost:1988) (username/password: haproxy)
- Elasticsearch HTTP [http://localhost:9200](http://localhost:9200)
- Kibana [http://localhost:5601](http://localhost:5601)
- Sense [http://localhost:5601/app/sense](http://localhost:5601/app/sense)
- Mesos [http://localhost:5050](http://localhost:5050)
- Marathon [http://localhost:9090](http://localhost:9090)
- Vamp [http://localhost:8080](http://localhost:8080)

If you run on Docker machine, use `docker-machine ip default` instead of `localhost`.

> **Note:** This runs all of Vamp's components in one container. This is definitely not ideal, but works fine for kicking the tires.
You will run into cpu, memory and storage issues pretty soon though. Also, random ports are assigned by Vamp which you might not have exposed on either Docker or your Docker Toolbox Vagrant box.  

Now proceed to our [getting started tutorial](/documentation/guides/).

Things still not running? [We're here to help →](https://github.com/magneticio/vamp/issues)
