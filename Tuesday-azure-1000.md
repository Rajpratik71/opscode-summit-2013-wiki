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

Different use case for auditing - customers have straight guidelines for change management - ITIL/SA16 - for compliance purposes.  Hook would be perfect for this.  System to Hook into: Tivoli event manager, Logstash, stated.  Need something out of the box.