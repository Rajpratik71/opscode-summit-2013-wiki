ChefSpec 3
==========

## Convener

[Seth Vargo](https://twitter.com/sethvargo)

## Participants

## Summary of Discussions

ChefSpec 3 has been released!  Pretty stable now.

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

Primary goal of ChefSpec 4 - provide integration level matching
Test kitchen runner will be more like ChefSpec at a higher level

ChefSpec 3 supports Windows (for example, Windows doesn't have curl, so something else is needed)

Personally despise Minitest matchers, but willing to add that if you have good ideas.

Should be packaged in the Chef Development Kit (Chef Omnibus, but for development & toolchain) as the standard way to test cookbooks.

Questions
=========

What do you mean by "higher level" tests?  Idea would be able to pull in nagios tests instead of integration level tests.

What's the difference between ChefSpec and ServerSpec?  ServerSpec wasn't designed to work with test-kitchen.  You end up re-writing the definitions you've already made in Chef (that being said Seth writes most of his tests right now in ServerSpec).  ChefSpec 4 would address this deficiency (if it supports integration-level tests).  Write monitors as tests.

Issues upgrading?  ChefSpec 3 already deprecates shift syntax, so no issues migrating from 3 to 4.

Testing an LWRP?  How do you do it on the unit level?  Nested cookbook with stupid little recipes embedded.  Unfortunately Chef really wants to read files from the file system in a directory tree.  Berkshelf doesn't address this issue.

Do you have access to the cookbook path?  Seems hard to manage.  LWRPs are hard because of the way that they are dynamically instantiated in Chef.  If you dynamically create cookbooks it's hard to figure out where it fails - then you start commenting out tests to find out what is broken.  Host file cookbook has a good example.

Should I wait for ChefSpec 4 to come out before starting to use ChefSpec?  ChefSpec 3 is super-stable, so it is definitely worth looking at.  ChefSpec 2 is not, so avoid that one (if you aren't using Chef 11).

What about code coverage?  Simplecov & Rcov won't work because Chef force reloads constants, which breaks all current code coverage tools.  Can't even parse YAST tree.  Worse in LWRP.  Not easy to do code coverage in Chef unit tests, even though it would be good to know how much of your cookbook is tested.

Where does ChefSpec fit in with RSpec and pure Ruby test tools?  ChefSpec uses RSpec, it just adds a bunch of Chef-specific stuff on top.

Which cookbooks should I look at to get started with ChefSpec?  Look at examples in the ChefSpec project first.  Rsync cookbook is a good example (it uses ChefSpec 2, but the syntax is similar in ChefSpec 3).  Bacon cookbook as well.

Can you use TravisCI to kick off ChefSpec tests?  Seth wrote a tool called strainer (but doesn't use it anymore).  Trick is to use something else to launch Test Kitchen from TravisCI (like EC2).  If you job takes longer than 40 minutes it will get kicked from TravisCI.  Short-term solution as Opscode intends to have a TravisCI-like service for Chef. 

## What will we do now?  What needs to happen next?

Write librarian integration (won't write software for a tool not use).  Would like someone who uses librarian to work on it.

Add ChefSpec to community cookbooks (talk to Sean O'Meara)

Make NTP cookbook an example of ChefSpec use.