---
layout: post
title: "Running Jenkins in Docker Containers"
date: 2015-02-11 22:44:25 +1300
comments: true
categories: [docker,jenkins,'continuous integration'] 
---

->{% img {{root_url}} /images/jenkins_logo.png %} {% img {{root_url}} /images/docker-logo.png %}<-

Finally I found some time to investigate running [Jenkins](http://jenkins-ci.org/) in a [Docker](https://www.docker.com/) container. There is an [Official Jenkins Repository](https://registry.hub.docker.com/_/jenkins/) on the [Docker Hub](https://registry.hub.docker.com/) so I started by pulling the latest version:

` docker pull jenkins `

More information about this image can be found in the Jenkins website [Official Jenkins LTS docker image](http://jenkins-ci.org/content/official-jenkins-lts-docker-image) blog post by [Michael Neale](https://twitter.com/michaelneale). Curiously this post also has a link to [cloudbees/jenkins-ci.org-docker](https://github.com/cloudbees/jenkins-ci.org-docker) GitHub repository which contained a lot of useful information.

Running the official Jenkins image could not be simpler:

` docker run -p 8080:8080 jenkins `

At this point I decided to implement a [Data Volume Container](https://docs.docker.com/userguide/dockervolumes/#creating-and-mounting-a-data-volume-container) to provide simple back-up capabilites and to experiment with extending the official image to include some plugins via the core-support plugin format.

<!-- more -->

## Adding a [Data Volume Container](https://docs.docker.com/userguide/dockervolumes/#creating-and-mounting-a-data-volume-container) 

Creating a named data volume container was pretty simple:

` docker create -v /var/jenkins_home --name jenkins-dv jenkins `

This command uses the '/var/jenkins_home' directory volume as per the official image and provides a name 'jenkins-dv' to identify the data volume container.

To use the data volume container with an image you use the '--volumes-from' flag to mount the '/var/jenkins_home' volume in another container:

` docker run -d -p 8080:8080 --volumes-from jenkins-dv --name myjenkins jenkins `

Once you have the docker container running you can go to [http://localhost:8080](http://localhost:8080) to see the Jenkins instance running. This instance is storing data in the volume container you set up previously, so if you set up a job and stop the container the data is persisted. To prove this you can stop and remove the 'myjenkins' container and start a second container:

` docker run -d -p 8080:8080 --volumes-from jenkins-dv --name myjenkins2 jenkins`

Once more hitting [http://localhost:8080](http://localhost:8080) will show your Jenkins instance but this time any jobs you set up and that were stored to the data volume container should be present.

## Building a Custom Image including some Plugins

Deriving a new [Dockerfile](https://docs.docker.com/reference/builder/) from the official image makes it simple to include some defined plugins. As per the documentation in the [Installing more tools](https://github.com/cloudbees/jenkins-ci.org-docker#installing-more-tools) section of the cloudbees documentation I created a Dockerfile with the following content:

```
FROM jenkins
MAINTAINER Pete Sellars <psellars@gmail.com>

COPY plugins.txt /usr/share/jenkins/plugins.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt
```

This expects a 'plugins.txt' file that in my case looked like this:

```
dockerhub:1.0
disk-usage:0.25
```

I then built my derived image in the folder containing both these files using the following command:

` docker build -t psellars/jenkins .`

Using this image I was then able to create a container that used the previously created data volume container:

` docker run -d -p 8080:8080 --volumes-from jenkins-dv --name custom-jenkins psellars/jenkins `

This container will have the [DockerHub Plugin](https://wiki.jenkins-ci.org/display/JENKINS/DockerHub+Plugin) and [Disk Usage Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Disk+Usage+Plugin) installed and any jobs set up in the previous containers. You could create a data volume container based on the custom image - and I would recommend this as a task to be done.

## Backing Up

To backup the data from the volume container is simple to. Simply run:

` docker cp jenkins-dv:/var/jenkins_home /tmp/jenkins-backup `

Once this operation is complete on your local machine in '/tmp/jenkins-backup' you will find a 'jenkins_home' directory backup. You could now use this to populate a new data volume container.
 
