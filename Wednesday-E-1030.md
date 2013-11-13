Chef dependency graph resolution, it's not Bundler
=============

## Convener
Sean Escriva

## Participants
Chris Roberts
Aaron Baer
Mike Weinberg
Jaime Winsor
Seth Falcon
Jesse Nelson
Matthieu Sauve-Frankel
...

## Summary of Discussion
An issue arises in testing clusters of infrastructure where a cluster depends on different versions of cookbooks and current dependency resolution tools fail to properly address multiple dependency graphs. Environments are named wrong. They can be used to describe policy for the dependency graph and enforce correct constraints.

But we're not talking about running multiple conflicting versions on a single node. That's crazy talk. Accurately modeling a full cluster of infrastructure on a developer workstation does not work with current tools if there are dependencies on multiple versions of the same cookbook. The Bundler style resolution assumes a single graph, current tools could be improved to handle a more complicated graph.


Ideal example commands might be:

* `berks resolve`
* `librarian-chef resolve`
* `vagabond kitchen test --cluster some-new-cluster`