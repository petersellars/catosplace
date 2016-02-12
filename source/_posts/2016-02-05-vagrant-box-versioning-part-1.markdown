---
layout: post
title: "Vagrant Box Versioning (Part 1)"
date: 2016-02-05 22:14:38 +1300
comments: true
categories: [atlas,vagrant,versioning]
---
TODO: Add Vagrant Boxes Image   
[Vagrant][] Box Versioning enables people who make boxes to push updates to boxes, and consumers of a box to have a simple workflow to check for updates, for updating boxes and determining what has changed in a box. Versioning is especially important and helpful if you work on a team. If you create or plan to create your own boxes then learning how to version boxes is very important. [Vagrant Box Versioning][] is designed to be easy to use and fit nicely into the Vagrant workflow. 

In this post we will explore the use of versioned boxes using [Atlas][]. Part 2 will provide information and good practices to use when versioning your own custom boxes using private host capabilities.    
<!-- more -->
## Versioning A Box
TODO: Add Versioning Image   
The easiest way to enjoy box versioning is to host your [Vagrant][] box on [Atlas][]. Boxes can be added to [Atlas][] using [Packer][], via the [Atlas][] web interface or using the [Atlas][] [Boxes API](https://atlas.hashicorp.com/docs/boxes). All of these options require you to [sign up for Atlas][https://atlas.hashicorp.com/account/new).  
 
## Viewing Box Information
TODO: Add Box Information Image   
...
## Checking For Outdated Boxes
TODO: Add Outdated Box Image   
...
## Updating Boxes
TODO: Add Updating Box Image   
...
## Removing Old Versions Of A Box
TODO: Add Removing Old Versions Image   
...

What about if you are unable to use [Atlas][] to host your [Vagrant][] boxes? For whatever reason you need to host boxes privately but still want to enjoy the benefits that versioning your [Vagrant][] boxes provides. In Part 2 of this article we will explore how this can be done and share some good practices to use when versioning privately hosted boxes.
### References
Box Versioning, Vagrant Documentation https://www.vagrantup.com/docs/boxes/versioning.html    
Creating a Base Box, Vagrant Documentation https://www.vagrantup.com/docs/boxes/base.html   
Creating a New Vagrant Box, Atlas Documentation https://atlas.hashicorp.com/help/vagrant/boxes/create   
Box Versioning and Lifecycle, Atlas Documentation https://atlas.hashicorp.com/help/vagrant/boxes/lifecycle
[Atlas]: http://atlas.hashicorp.com	
[Packer]: http://www.packer.io
[Vagrant]: http://www.vagrantup.com
[Vagrant Box Versioning]: https://www.vagrantup.com/docs/boxes/versioning.html
