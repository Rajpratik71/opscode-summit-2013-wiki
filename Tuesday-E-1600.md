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

## What will we do now?  What needs to happen next?