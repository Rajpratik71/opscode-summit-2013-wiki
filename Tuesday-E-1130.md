Opscode Open Source Strategy and Pushy
=============

## Convener
[Barry Crist](https://twitter.com/barry_crist)

## Participants
[Kevin Smith](https://twitter.com/kevsmith)  
[Kevin Knoepp](https://twitter.com/kevinknoepp)  
[Jim (Thor) West](https://twitter.com/medieval1)  
[Adam Vinsh](https://twitter.com/adamvinsh)  
[Gregoire Seux](https://twitter.com/kamaradclimber)

[Jérémy MAURO](https://twitter.com/criteo)  
[Jeffrey Hulten](https://twitter.com/jhulten)  
[Adam Jacob](https://twitter.com/adamhjk)


## Summary of Discussions

**Pushy will be open sourced**, the date has not been decided.

### What is Pushy?
* Operates over ZeroMQ
* Uses same REST security/trust model of Chef
* Basic node presence information (node up/down)
* Run operations (chef-client) as jobs on multiple systems
* Requires Chef Server 11
* May work with Chef Client 10?

### Future
* Streaming job output

### Opscode strategy for open sourcing projects
* ...
* ...
* Value in proliferation
* Other considerations

### Locking
* How to perform resource locking?
* Controlling number of nodes?
* Mutex?
* Delayed notification, with a lock, timeout?
* Distributed systems

### pushy vs knife ssh 
* zeromq instead of ssh (transport)
* rest authentication instead of ssh
* doesn't need direct network access
* able to require quorum

## What will we do now?  What needs to happen next?