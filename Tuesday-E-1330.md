ChefSpec 3
==========

## Convener

[Seth Vargo](https://twitter.com/sethvargo)

## Participants

## Summary of Discussions

What happened between ChefSpec 2 & ChefSpec 3?

Seth started working on ChefSpec with the original author.  Identified where the code was terrible with backwards compatibility and technical issues.

ChefSpec 3 requires Chef 11+, does not work with prior versions.  Must use ChefSpec 2 for older versions of Chef.

ChefSpec 3 focused on speed - resource caching, builtin caching, leveraging resources.

Custom matchers now available in ChefSpec 3.  Can automatically pull in custom matchers.

ChefSpec 3 does dependency resolution automatically with Berkshelf - better Berkshelf integration.

`describe recipe` and `describe cookbook` as recommended primitives.



## What will we do now?  What needs to happen next?
