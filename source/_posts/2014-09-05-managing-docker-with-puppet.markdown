---
layout: post
title: "Managing Docker with Puppet"
date: 2014-09-05 19:29:32 +1200
comments: true
categories: [Puppet,'Configuration Management', Docker] 
---
I have been using [Puppet](http://www.puppetlabs.com) for a number of years now and it is the configuration management tool I feel most comfortable using. Recently I have been investigating how to utilise [Docker](http://www.docker.com) during development and in Continous Delivery Pipelines.

Puppet offers a couple of ways to manage Docker itself and Docker Containers. PuppetLabs recently produced a webinar [*Puppet &amp; Docker:Using Containers with Configuration Management*](http://puppetlabs.com/webinars/puppet-docker-using-containers-configuration-management) featuring [James Turnbull](http://www.twitter.com/kartar)(__Docker__) and [David Lutterkort](http://www.twitter.com/lutterkort)(__PuppetLabs__)

<!--more-->

The webinar had the following agenda:

 - Overview of Docker Containers
 - Puppetizing Docker Hosts
 - Authoring Docker Images with Puppet
   - without a master (_puppet apply_)
   - with a master (_puppet agent_)
 - Running Puppet within Containers

The overview of [Docker Containers](https://docker.com/whatisdocker/) was provided by James Turnbull who outlined the difference between virtual machines and Docker virtualization. He emphasised the speed and performance benefits of Docker Containers vs virtual machines, the ease of use Docker provides compared to other container implementations and the view that Docker has a vital role to play in the developer workflow.

> much more than a provisioning story...

*James Turnball - Docker and the Developer Workflow*

James also outlined the difference between mutable and immutable infrastructure and how Docker is well suited to mutable infrastructure. Docker has lightweight images compared to the traditional [Golden Image](http://searchservervirtualization.techtarget.com/definition/golden-image) and therefore the team had rehabilitated the image model. He also stressed the suitability of Docker for ephemeral instances, whilst configuration management is more suited for longer lived instances.

David Lutterkort then provided the Puppetizing Docker Hosts section. He recommened the use of [Gareth Rushgrove's Docker module](https://forge.puppetlabs.com/garethr/docker). This module enables the installation of Docker, management of Docker Containers and the ability to run docker containers with Puppet.

```puppet
class { 'docker':
  tcp_bind    => 'tcp://127.0.0.1:4243',
  socket_bind => 'unix:///var/run/docker.sock'
}
```

When authoring Docker Images with Puppet there are two options:

1. Without a master (*puppet apply*)
2. With a master (*puppet agent*)

When building the Docker container a ```puppet apply``` is used in the Dockerfile. This has the disadvantage of requiring a clean-up of the image to remove excess baggage once the configuration has been carried out. It also has some security implications.

When using a Puppet master a puppet directory is copied into the container which includes a [puppet-docker script](https://github.com/lutter/puppet-docker). This puts the SSL certificates in the right place, sets some facts and is promoted by David Lutterkort as the most natural way to build Docker Containers.

Running Puppet within Containers requires the need to install an init system into the Docker Container.

The Q &amp; A session is well worth listening too, amongst other things discussed are the best tool to use for installing packages into containers, how to distribute private docker instances, how does Docker improve your architecture and when to use a DockerFile or a module.

[Librarian-Puppet](https://github.com/rodjek/librarian-puppet) appears best suited to package installations into Containers, the [Puppet module tool](https://docs.puppetlabs.com/puppet/latest/reference/modules_installing.html) being overly simplistic whilst [R10k](https://github.com/adrienthebo/r10k) is probably too heavyweight. 

The [Docker Hub](https://docs.docker.com/docker-hub/) service can be used for private repositories or behind a firewall you can run the [Docker Registry](https://github.com/docker/docker-registry) - an image store. Architecture wise Docker can help provide more scalable Developer environments and even enable building out your own PAAS architecture.

> A DockerFile is little more than a collection of directives. Large DockerFiles can soon start to display _'Golden Image'_ traits. Using Puppet modules addresses this issue...

*David Lutterkort - On When To Use DockerFiles vs. Modules*  
