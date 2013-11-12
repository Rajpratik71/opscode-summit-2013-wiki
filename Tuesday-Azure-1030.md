Introduction to Crowbar
=======================

## Convener
Judd - Dell guy

## Participants

## Summary of Discussions
What is crowbar?
Two and a half years ago colleagues tried to install
OpenStack.  Hellish to install OpenStack.  Gear still in boxes
nothing was going on.

Crowbar focused on bringing up new gear - so you don't f*ck it up and have to go back into the datacenter

Straight DHCPD, no cobbler

Crowbar 1 - being demoed now

Crowbar 2 - more sophisticated state model

46 people working on Crowbar team at Dell

Admin node

TFPD server - straight

Run chef client again to fix up

Chef is used as the back end database.  Issues catching up with node changes when Chef is used as the back-end db.  Will change in Crowbar 2.

Crowbar 2 - Postgres database & Chef 11

Crowbar 1 - Chef is database & Chef 10

Running discovery image in RAM, can bring up a whole new rack of gear

In memory CentOS images run on nodes pulsing to announce node has been brought up - don't need hard drive installed in gear

Allocate - reboot node and apply BIOS settings

OpenStack SWIFT best to use JBOD not RAID

Reference architecture

720 bread and butter cloud gear

820 big beefy database boxes

Ironic - does not do RAID and BIOS

Ironic allocate bare metal

Full control of IPMI - changes IPMI password

UEFI WSMan new metal standards for configuring BIOS

github.com/crowbar

Barclamp

Whole lotta Chef and some bash

barclamp-dell_raid

Partial Rails app RailsEngine

Data bags get aloaded to inform barclamp on how to do it

Databags for a bunch of expected drive layouts

Neat thing about BIOS barclamp - will reorder NICs for you (despite what PCI bus thinks it should be)

How to customize OS install?  Use dev tool.  Can't assign kickstarts/preseeds per OS/MAC address, only by software stack

Need crowbar development environment

dev tool

Large shell script

Discovery image - sledgehammer

Pulls down image

Dev has commands to customize OS image among other things

Does it do Windows?  No, but deploying OpenStack with Hyper-V

Automatically deploys Ganglia and some other tools.

Does it scale?  Crowbar backs off when you try to scale horizontally

Crowbar is a bar clamp of itself

Conduit - flexible network attributes/specify bus order

How do you handle race conditions in network device name?  Crowbar abstracts it out.  Will force Ubuntu and SUSE to do the right thing.

Does crowbar serve the purpose of being a network inventory server?  Database is what is coming from ohai in the Chef server (even with Postgres it's just Chef data) - depends on what you want to do with the inventory (not really for the accountants or to collect historical data).

Uninstall - not supported

SUSE added patch to Crowbar 1 so you can see Chef run output graphically

Bulk Edit area - holding pen for new nodes.  Can be used to dump new configurations.

If you take any box, custom hardware, are there any caveats?  No if the box supports IPMI.  Better if box support WSMan.  Will work on nearly all gear.  (Can work on non-IPMI boxes sometimes - will back off to ACPI)

UEFI support is in

Is there any concept of deploying grouping of boxes, say a cluster of nodes without doing each box individually?  Swift is a good example of that - proxy nodes vs. storage nodes, plus storage nodes have roles.  Can assign roles to whatever number of servers you want.  Takes a software/service-first mentality.  Don't have to build a node all at once - can build it gradually.

Overlap in work with what the Razor people are doing.  Razor is annoying because they are using Facter.  Sledgehammer - all sledgehammer bits are in the crowbar repo http://github.com/crowbar/crowbar  Don't remember where Sledgehammer actually is because apparently it has moved.  Has chef-client in it plus Dell bits.

Is there a pattern to scale the management node?  It's just nginx.  Edit the crowbar barclamp to add a proxy to the nginx node.  Upgrade github repo and pull from source or update package from cache.

## What will we do now?  What needs to happen next?

Will be demoing Crowbar 2 tomorrow and recap today