Containers - Docker, LXC, Zones
=============
In which we explored how people are using containers in their infrastructure, ways in which they're looking to do so,  best practices that are emerging, and how Chef fits into this. 

## Convener

* Marc Paradise - Opscode 
* Chris - Yahoo!

## Participants

## Summary of Discussions

Containers are being used and explored in a variety of scenarios
* application deployment into a specific replicable base environment
* minimal configuration, single application containers 
* quick time to bring up an application: containers deploy quickly 
  and come up no or minimal convergence time. 
* an extra level of security to effectively isolate applications
   
There are a few patterns emerging in usage, both with and without chef: 
* creation of 'golden image' for near-instant deploy 
    * create AMI (container image, etc...) with chef or chef-solo 
* configuration of the container with a minimal chef run after creation
    *  full chef run, chef local mode, chef-solo 
* chef used to manage container hosts, provide and maintain underlying 
  infrastructure
* packer emerging as a possibility for create-once, deploy-anywhere
  images - still under development. 

Some things haven't been resolved: 
* service discovery - though this is not really a new problem, it 
  becomes more apparent when the cost to bring an image online is 
  measured in seconds instead of minutes.  Zookeeper, etcd, and 
  DNS being used (or experimented with)
* consistent practices for capturing persistent data (logs, etc) from a
  transient container.  

## What will we do now?  What needs to happen next?

The idea of chef providing support for containers as first-class citizens was raised a few times, such that chef could manage provisioning the container, starting/stopping it, configuration of it. 

