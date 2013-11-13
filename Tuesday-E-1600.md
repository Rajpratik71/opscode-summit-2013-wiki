Test kitchen - a discussion
===========================

## Convener

[Fletcher Nichol](https://twitter.com/fnichol)

## Participants

## Summary of Discussions

Would like to talk about Test Kitchen, not a demo

Lots of people are using Test Kitchen

When is 1.0 coming out?  It could have been shipped 8 months ago.  Not a lot has changed.  Big hangup is documentation - want sufficient documentation ready before 1.0 release and reasonable documentation.  Fletcher doesn't scale to onboard people on to Test Kitchen.  Hopefully in the next week or so want to get docs ready.

Need to fix Chef Zero provisioner - Test Kitchen doesn't know it is available to it yet

Opscode merged a bunch of work to make Test Kitchen work better with non-Unix Linux to work better with bourne shell.  Using Test Kitchen to Juniper test network switches (JunOS is transactional).  Will allow us to test against some old Sparc Slaves.  Now we can use Test Kitchen for nearly everything internal to Opscode.

What form is the documentation going to take?  Readme/wiki?  Do you need help?  Plan to have standalone web site for Test Kitchen, not a 3000 mile long README.  A reasonable getting-started guide.  Want to have getting started guide similar to [Packer](http://www.packer.io/intro).  Page per concept.  Found that almost nobody likes writing docs.

The Test Kitchen repos are going to be split into it's own Github community.  All the drivers and gems will all be in one place.  Similar to Guard or Jenkins community.  (Also a Berkshelf organization).

Don't wait on the 1.0 release to start looking at it.  It won't change very much before release.  There's been some minor gem dependency issues (celluloid).

Opscode is moving away from bats in Test Kitchen.  Standardizing on ServerSpec for integration testing (because engineering team uses RSpec).

Bats was an experiment for a plugin.  Simplest was to write a shell script for a test.  Was capturing test knowledge in shell code.  Once you go multi-platform it gets more difficult to use shell scripts.  Not that you can't mix multiple test runners.  If bats is working for you, it's great.

Serverspec is great because it works on Windows - has WinRM built into it.

After 1.0, want Windows Guest support and multi-provisioner support for Test Kitchen (like Puppet!)

Spent more time working with the Docker driver if you are using Debian or Ubuntu.  With Docker you have a golden base, then have snapshots taken all the way.  Can have multiple snapshots with all the versions you want to support and can quickly test multiple platforms at once.

Docker with an http cache makes Test Kitchen usable on cafe wifi

Possibly need to work out issues with Chef Zero and using older versions of Chef.

Anyone using the Test Kitchen EC2 driver?  You can rack up a huge bill.  You need to use destroy=true.  Digital Ocean driver for Test Kitchen - has per minute billing unlike Amazon.

Pete has been working with Julian to create FreeBSD boxes for use with Test Kitchen: https://github.com/opscode/bento  Test Kitchen will soon magically be able to pull down FreeBSD boxes.

Has anyone tried writing a driver?  Ideas for drivers - zones, chroot & FreeBSD jails - a fully-contained environment.

BOSH - Helpful for deploying CloudFoundry

Neat trick  - you can use ERB templates in your .kitchen.yml to handle multiple platforms.  [Miah has an example of this technique in her .kitchen.yml files](https://github.com/miah/chef-redis/blob/master/.kitchen.yml).  This is a helpful way to avoid big-ass .kitchen.yml files.  Many people were hoping to avoid having big-ass Vagrantfiles with all your platform-permutations and this is a technique unique to Test Kitchen.

How do you run the same runlist against different drivers - right now use environment variables for this (or symlinks).  Might be nice to have the driver separate from the suites so you don't have to combine it.  For example, switching between docker and vagrant.  Another technique, a $HOME/.kitchen/.kitchen.yml can provide some defaults to override.  Can also be used to configure reasonable defaults for vagrant basebox URLs and EC2 AMIs (for vagrant).  Kitchen-EC2 now has a big list of AMIs in it as .JSON to work across all the regions.  Now you should be able to scrub through drivers with multiple ease.

What about multiple BM Test Kitchen runs?  There is Vagabond with LXC.  Might be easy to add suite dependencies and run erchef on the host to run the suite.  (Fletcher is groaning).

Jon Kaiser who did Chef Zero is developing an abstraction of an instance running a thing for testing enterprise Chef topologies (chef-restuarant).

Test Kitchen isn't trying to solve the test dependency problem.  Vagabond isn't a good solution outside the Linux world.  Possible to use Test Kitchen as a Ruby library (not too much code and is structured in a way so that's possible - was working work Stephen Nelson-Smith to using test instances and drivers this way to describe how to create nodes and wire them together - test kitchen can be plumbing - and it worked pretty well).  You can also override the data loader if you don't like YAML, for example.  Played with Sean to override stuff in Ruby code rather than Gem/YAML.  Test Kitchen doesn't have the mechanics to know which node comes up first, though.   Was intended to test a single cookbook standalone.  chef-solo can have a nodes directory with IP addresses to fake it out.  Not really intended for cluster testing yet.

First time Test Kitchen - difference between `kitchen converge`, `kitchen test`, `kitchen verify'.  What's the difference between test and verify.  Test transfers files to the node so they're fresh, verify does not.  By default `kitchen test` automatically destroys (can be overridden), unless the test run fails (except with the EC2 provider).  That being said, carefully monitor EC2 usage.

How does Test Kitchen know about dependent cookbooks?  What if A calls B, how does Test Kitchen know about that?  Test Kitchen is Berksfile aware - it will haul stuff in.  Test Kitchen abuses Berkshelf in that it just uses the dependency resolver to copy cookbooks in via scp.

What about using Test Kitchen to test post-deploy?  I'd rather write one set of tests with Test Kitchen?  The Opscode consulting team is experimenting with this with a proxy driver.  This is where it is handy to use Serverspec as you could tell it to run in different places.  Cookbook tests tend to translate pretty well to post deployment monitoring tests (like flapjack cucumber).  Jamie is also using Elixir runners as performance tests as well.

## What will we do now?  What needs to happen next?