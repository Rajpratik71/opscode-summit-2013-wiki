Cookbook Development Toolsets
=============================

## Convener

[Charles Johnson](https://twitter.com/chipadeedoodah)

## Participants
jim (Thor) west
, ...

## Summary of Discussions

## Chef DevKit Manifesto 

Vagrant and Berkshelf have become the de-facto Chef development workflow, but it is not properly documented.

Plus, getting your Chef Development Workstation environment kinda blows with all these extra tools.

There's a whole mess of tools and it's hard for people who are new to Chef (or if you drop your laptop).  Have a shell script to setup the Chef cookbook-writing environment.

Problem hasn't been solved because people skip straight to implementation (wrapped in an MSI installer, utensils omnibus, etc.)

Would like to create a manifesto at a high level on what a Chef development environment should look like.  Want to define some specs for a Chef DevKit, define them and let it evolve.

Start of the manifesto:

* Should have defined product owners
* Should support all major OSes first-class: Win/Linux/Mac OS X
* Should cover everything prior to code commit (workstation)
* Should be packaged
* Should come packaged with testing tools
* Should proscribe workflow
* Should evolve
* Should work behind corporate proxies
* Should be defined by the community
* Should dovetail with the work being done on the Cookbook Style Guide

Owners should be both in and outside Opscode - history has shown that the Opscode-recommended workflow got blow of the water by Berkshelf/Jamie Winsor of Riot Games.  Community-defined standards are better than the organized-proscribed ones

Stop leaving Windows out in the cold

Ansible is kicking Opscode's ass on getting set up quickly.  We can do better and be even easier to set up.

Tools shouldn't fall down if you have a f*cked up firewalled environment with no access to the community cookbooks.

## How to build something on top of Chef

Problem people run into:

* What attributes should I expose? (chef solo vs. chef server vs. platform)

Should we be building tooling on top of Chef on top of this?

Define standard metadata for cookbooks?



## What will we do now?  What needs to happen next?

Meet in quiet room after this session.  Want to flesh out the manifesto and assign product owners