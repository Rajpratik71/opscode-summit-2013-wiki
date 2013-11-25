Session Title
=============

## Convener

## Participants

## Summary of Discussions

* Ensure proper order of operations for setting up / upgrading servers
People don't always follow the directions, and do things like
upgrading a backend secondary before anything else. Sadness ensues.
* Something like CREST would be really good for multi-machine setups
https://github.com/kevsmith/crest
* Customers don't always like DRBD
They've been burned in the past, they have other solutions in use
already, etc.
* Express requirements in terms of capabilities, not specific hardware
e.g. "For HA, you need a maximum latency of X ms between your
backends", not "you need two servers connected with a crossover
cable"
* Abstract out HA "interfaces" and let customers choose their own implementation
Not everyone wants DRBD + Keepalived
* Speak in terms of "case studies"; let customers decide their setup
e.g. for each topology we support, describe a particular setup and
show its performance characteristics under given loads (e.g., X
chef-client runs every Y minutes). Show how various tuning
parameters can affect performance on these setups.
* Give tools for PostgreSQL
DBAs would like to know the schema, etc.
* Provide performance testing tools to customers
Let them experiment with their own hardware to determine their own
optimum setup. They could set up an EC server, create load using
the perf tool, and experiment with different topologies, hardware,
tunings, etc. until they got a setup they were happy with. Then,
they wipe the server clean and start using it with their own data
for real.
* Provide scaling of individual services
Currently we lump all "backend" services together on one set of
boxes, and all "frontend" services on another. Some customers have
expressed a desire to be able to scale things in a more granular
manner. For example, placing bookshelf on its own machine(s),
separate from the PostgreSQL / CouchDB machine(s).
* Expose performance data for monitoring
How do customers know what their EC services are doing?!
* How could we provide datacenter-level HA?

## What will we do now?  What needs to happen next?


