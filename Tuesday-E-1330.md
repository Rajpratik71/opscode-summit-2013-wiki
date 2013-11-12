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

All documentation is now inline using yard and is generated.  Documentation online is most current.  Docs are versioned with the gem so you'll get the documentation corresponding to the version you have installed.

Testing against a huge Travis CI matrix.  Build should now be green all the time.

Roles and databags are now top-level macros so easier to use in ChefSpec 3.

Abandoned semantic matchers - action_resource - better matching between what you are writing in Chef vs ChefSpec

Breaking change - render file matcher doesn't exist anymore.  In ChefSpec 2 this could refer to multiple things.  With Chef 11 files became a first-class resource, now there is a `create_file` matcher and a chainable matcher.

Every resource matcher is now chain able (`with_gid`, `with_owner`, etc.)

Testing LWRPs - documented in README.
Testing roles - documented in README.

ChefSpec 3 is very extensible now, well-tested, with lots of examples.

Currently uses `chef-solo` under the hood.  Will change in ChefSpec 4 to use `chef-zero`.


## What will we do now?  What needs to happen next?