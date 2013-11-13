Top 3 Requests from Opscode
=============

## Convener
Kevin Knoepp  

## Participants
Julian Dunn  
Bryan McLellan  
Ranjib Dey  
Matt Ray  
Dan Deleo  
Tim Dysinger  
Doug Ireton  

## Summary of Discussions
* ruby 2.0 in omnibus
* drop ruby 1.8.7 support
* fix JSON dependency
* resources for managing containers
* knife-cloud plugin refractors
* CHEF-2913 track changes to an attribute for debugging purposes
* version objects (roles, data bags)
* semver support for cookbook versions
* API generated audit trail
* omnibus packages hosted by chef server (omnitruck? Bootstrapper?)

Ordered list: 
## What will we do now?  What needs to happen next?

Chef 12 Features
================

Chef 12 Feature discussion

Listed on community summit page
https://wiki.opscode.com/display/chef/Suggestions+for+2013+Community+Summit  

Ruby 2.0 Support / Omnibus with Ruby 2.0

Versioned Attributes

Taking away Ruby 1.8.7 Support in Chef 12

Just use core JSON (Yagile in core Ruby)

Make error messages not terrible (at character 80 there was an error)

Fix JSON

Get rid of Yagile use core JSON

Yagile is seems to be abandonware

Does Ruby 2.0 work on Windows (When Ruby 2.0 first came out, compiled version of the libraries switched on 1.8 
to 1.9 binary compatibility, so existing gems didn't work until you compiled them yourself)

Chef 12 support in a post-container world (Docker LWRPs) - John Kaiser working on low-level machine abstraction

LXC components now namespaces, need to support that - route, ifconfig, etc.

Opscode does not want to tackle tools that manage network or storage

Database agnostic - tied to Postgres?  Tried this with hosted in Percona build of MySQL - didn't work with a database abstraction.  Don't want to waste time doing workarounds with MySQL - also not going back to CouchDB ;-)

Better support for node attribute debugging in [CHEF-2913](https://tickets.opscode.com/browse/CHEF-2913) - Provide tracing of attribute changes at runtime

## Feature suggestions

Versioned roles and environments

Versioned databags

Cluster definitions - add cluster as a first-class data structure (covered by John Kaiser work)

Clean up dynamic use of EC2 nodes used, polluting the Chef server - remove nodes that are no longer provisioned, etc.  Perhaps add TTL field to node.  Right now people need to run cron jobs to clean things up.  Might be a more generic solution around cleaning up old things - like pruning old cookbook versions.  Garbage collection on version policy.

More flexible cookbook versioning, more than x.y.z, perhaps prerelease, rc1, rc2, etc.  Automatically keep change log.  Perhaps fully support server spec fully?  Currently there is Opscode [semver](http://semver.org).

API generated audit trail for changes to the system - who f*cked up production.  Better if specialized for auditing and not just another log file.  Want audit trail on everything the system touches.  Also would be good to have hooks and events to build an auditing system.

Important to know when someone pushes a cookbook or uses `knife node edit` - who did it - for auditing, so that processes can be put in place to manage.  Right now don't know who changed what.

Different use case for auditing - customers have straight guidelines for change management - ITIL/SA16 - for compliance purposes.  Hook would be perfect for this.  System to Hook into: Tivoli event manager, Logstash, stated.  Need something out of the box.  There is a lack of documentation on how to write event/report handlers.  Most people don't know event handlers exist.

Local mirror of chef installers/bootstrap template.  Opscode has tool - Omnitruck which does this, but doesn't solve the problem.  Customers need apt/yum repo with the server to distribute to thousands of nodes.  Nice to have local mirror of agent install and don't have to curl a bash script across the internet to install the chef client.

Not just about packages.  People need to follow the same packaging directions - set up a proxy attribute so you have the same experience inside/outside.  Perhaps handle on workstation not server.  Bootstrap templates are bad idea - copy secrets into argv of the process, not secure.  Perhaps get rid of validator key - you should be able to use your own key.

Hard to control how Chef gets installed in bootstrap templates.  For example try to install a machine with omnibus packages of a different version, or machine that doesn't talk to the internet.  Don't want to set up a new omnitruck server with these hacked things.  Instead bootstrap the machine and say that you have a package somewhere here.  `knife bootstrap` uses `knife ssh` as a library - difficult to copy over, and conflicts with EC2 command line arguments - hard to write an ssh script to bootstrap.  In anger, Dan has been rewriting all that as the bootstrapper project.

Bootstrapper - has a template defined of what you want on a node.  Sharing a file instead of documenting what the right command line parameters are.  Breaking the installation into bootstrap config & transport that you can swap out, so you could install Chef differently by changing out one component.  Currently you can bootstrap a machine with it, but it needs polish.

The run action must die - Sean O'Meara.  Number one thing that comes up on the mailing list daily.  Running resources during compilation phase than during the convergence phase is more necessary in things like omnibus.  Right now things can suddly jump the line with different syntaxes.  Perhaps "run prerequisites".  Though when we need compile-time stuff, it's limited.  Perhaps don't let resources converge during compilation phase.  Right now Chef does this, perhaps it was a bad idea - flip bit in Chef 12.

Speaking of convergence, `error 412 precondition failed` should tell which cookbook(s) it failed on.  Right now you have to log into the server and dig into the stack trace.  Depsolver should at least add conflict resolution.

Recipe-level cookbook dependencies.  Getting locked into situations where there are a lot of dependencies when only using small portions of a cookbook.  Right now have to pull down everything.  People struggle with this a lot.  Like why need to download Windows.  And not just at the recipe level.  It's hard because Chef doesn't know what you're going to include.  Most people don't usually notice except when people see Windows - people don't like seeing Windows cookbook on say Solaris box.  Perhaps just move things like Windows support in core Chef so people don't see it.  Also perhaps split up cookbooks.  Don't get too focused on Windows - it's still a problem elsewhere.  Is it a cookbook problem or a chef problem?  For example Apache cookbook does way too much and might be better done in an LWRP.  A failed run blows away all cookbooks from the cache.   It downloads all the cookbooks the next time.

How long do you need to move off Chef 10?  6 months after getting Chef 11 into production.

## Votes on features

* Ruby 2.0 Omnibus - 14
* Knife Cloud Plugin Refactor - 4
* Versioned Objects - Everyone
* Semver Support for Cookbook Versioning - 2
* API Generated Audit Trail - 10
* Resources for managing containers - 8
* Omnitruck/yum/apt repositories - 20
* Depend on specific cookbook components - 1
* Do something about JSON - 5

## What's missing

* Ability to debug attribute changes in Chef
* Garbage Collection - 8
* Ability to freeze all cookbooks by default (no force - only get to upload it once) - 4
* Metadata dependencies/platform dependencies in data

Why is Ruby 2.0 voted so high?