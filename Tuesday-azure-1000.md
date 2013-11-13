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

Clean up dynamic use of EC2 nodes used, polluting the Chef server - remove nodes that are no longer provisioned, etc.  Perhaps add TTL field to node.  Right now people need to run cron jobs to clean things up.