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
* Should define convention

Owners should be both in and outside Opscode - history has shown that the Opscode-recommended workflow got blow of the water by Berkshelf/Jamie Winsor of Riot Games.  Community-defined standards are better than the organized-proscribed ones

Stop leaving Windows out in the cold

Ansible is kicking Opscode's ass on getting set up quickly.  We can do better and be even easier to set up.

Tools shouldn't fall down if you have a f*cked up firewalled environment with no access to the community cookbooks.

## How to build something on top of Chef

Problem people run into:

* What attributes should I expose? (chef solo vs. chef server vs. platform)

Should we be building tooling on top of Chef on top of this?

Define standard metadata for cookbooks?

Is this not the idea of the application cookbook?  Write a simplification cookbook/wrapper?

Web/interface wizard to define a skeleton cookbook

Scary to depend on the attribute documentation written by the developer.  Most cookbook documentation is simply a list of attributes.

Beginner version of cookbooks?

Example - apache cookbook covered the most general use case.  Now it's a zillion of different attributes & very hard for beginners to get started with it.

Is it too much abstraction to simply fill out a form to create a cookbook.

Training has evolved - have had more success training beginners to write simple cookbooks instead reusing community cookbooks.  Currently not very easy to reuse community cookbooks.

Split cookbooks like apache into simple and advanced settings?

Chef koans?  Git Real challenges from Code School.  Chef School?

Want to approach at a high level - how do I get a basic LAMP stack setup and deploy an application within it?  ( [PuPHPet](https://puphpet.com) or [SoloWizard](http://www.solowizard.com)

Besides Opscode most people don't care about having a cookbook that works on a zillion different platforms - just care about one.  Also only care about problems of their business, not problems of Chef.

[chef-rewind](https://github.com/bryanwb/chef-rewind) for modifying community cookbooks
http://devopsanywhere.blogspot.com/2012/11/editing-chef-resources.html

Sometimes it's just a matter of specifying local defaults rather than redefining the cookbooks

## Eclipse/IntelliJ integration - Oliver Ferrini

Created plugin for Eclipse to integrate chef-client.  Would like to know who uses an IDE on a regular basis.

Want to give unified user experience in your IDE of choice.

Brian has voted to get IntelliJ to add Chef support to RubyMine - getting highly up-voted.

Could package IntelliJ Community Edition with a Chef plugin and call it ChefMine, similar to [goide](http://go-ide.com/2011/08/09/goide_release_1_0_darwin.html)

[Puppet Geppetto](http://puppetlabs.com/blog/geppetto-a-puppet-ide)

1.0 Feature list for IDE integration

* Syntax highlighting
* Resource completion
* Testing framework (ChefSpec/ChefZero)
* Search completion
* Foodcritic/code linting
* chef-shell integration
* Test kitchen integration

Event-based code coverage - resource coverage vs. code coverage (given that code coverage seems hard to do)

Hard to figure out how to try to set things up.  Rails emphasis on convention vs. configuration.  Come up with convention that works 80% of the time.  Otherwise we will have a small group of people who are very, very good at this.  There's too many options right now.

## What will we do now?  What needs to happen next?

Meet in quiet room after this session to work on the DevKit manifesto.  Want to flesh out the manifesto and assign product owners
