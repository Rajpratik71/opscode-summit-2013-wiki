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



## What will we do now?  What needs to happen next?