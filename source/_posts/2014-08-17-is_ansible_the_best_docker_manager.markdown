---
layout: post
title: "Is Ansible The Best Way To Manage Docker?"
date: 2014-08-17 17:05:16 +1200
comments: true
categories: [Docker, Ansible, 'Configuration Management']
---
I sense that [Ansible](http://www.ansible.com "Ansible Website") is growing in popularity. [ThoughtWorks](http://www.thoughtworks.com "ThoughtWorks Website") now recommends the adoption of Ansible '*for automated control of your infrastructure*' in their industry recognised [Technologoy Radar](http://www.thoughtworks.com/radar  "ThoughtWorks Technology Radar").

>we continue to be impressed with its capabilities and ease of use compared to other offerings in this space

*ThoughtWorks Technology Radar - July 2014*

<!--more-->

I have been researching and experimenting with [Docker](http://www.docker.com "Docker Website") for a while, but have yet to really decide on a best way to manage it. Whilst looking into Ansible I was intrigued by their claim that:

> __Ansible is the best way to manage Docker__

*Ansible Website - [Ansible &amp; Docker](http://www.ansible.com/docker "Ansible &amp; Docker")* 

There is a video from [AnsibleFest NYC (May 2014)](http://www.eventbrite.com/e/ansiblefest-nyc-2014-tickets-10952628607 "AnsibleFest EventBrite") on the [Ansible &amp; Docker page](http://www.ansible.com/docker "Ansible &amp; Docker") outlining a number of [Ansible Modules](http://docs.ansible.com/modules.html "Ansible Modules Documentation") that support Docker management. Among them are the [*docker_image*](http://docs.ansible.com/docker_image_module.html "Docker Image Ansible Module"), [*docker*](http://docs.ansible.com/docker_module.html "Docker Ansible Module"), [*docker_facts*](http://patg.net/ansible,docker/2014/07/10/ansible-docker-facts "Ansible Docker Facts Module") and a [*docker dynamic inventory plugin*](https://github.com/ansible/ansible/blob/devel/plugins/inventory/docker.py "Docker Dynamic Inventory Plugin for Ansible").

|Module Name|Docker Use|Project Link| 
|--------------|----------|------------|
|*docker_image*|Add, Build or Remove Docker Images|[Ansible Docker Image Module](http://docs.ansible.com/docker_images_module.html "Docker Image Ansible Module")|
|*docker*|Start, Stop or Delete Containers|[Ansible Docker Module](http://docs.ansible.com/docker_module.html "Docker Ansible Module")
|*docker_facts*|Provide Ansible dictonary entries: docker_containers and docker_images|[Docker Facts Module](http://github.com/CaptTofu/ansible/tree/docker_facts "Ansible Docker Facts Module")
|*docker dynamic inventory plugin*|Manage elastic resources inventory &amp; provides a JSON output serving as an inventory list to use|[Dynamic Inventory Plugin on Github](https://github.com/ansible/ansible/blob/devel/plugins/inventory/docker.py "Docker Dynamic Inventory Plugin for Ansible")

*__Ansible Docker Modules__*

If these modules make Ansible *__'the best way to manage Docker'__* or not has yet to be determined by myself. My plan is to try out Ansible in the next couple of months - for Docker managent. I will update this post with my verdict after some experimentation. 

Ansible &amp; Docker, [Patrick Galbraith](http://patg.net "Patrick Galbraith's Blog"), HP Advanced Technologies Video

{% youtube oZ45v8AeE7k %}
