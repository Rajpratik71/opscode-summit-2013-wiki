Introduction to Crowbar
=======================

## Convener
[Judd Maltin](https://twitter.com/newgoliath) - Systems Principal Engineer @Dell

## Participants

## Summary of Discussions
What is crowbar?
Two and a half years ago colleagues tried to install OpenStack.  Hellish to install OpenStack.  Gear still in boxes
nothing was going on at customer.  Customer IT would take months to give us IP addresses.  CustomersNo DHCP, no PXE, nothing.  We needed to install our own.

Crowbar Admin server includes all the above.  It's focused on bringing up new (or re-used) gear - so you don't f*ck it up and have to go back into the datacenter

What's in the admin box:
* Crowbar Rails app/REST server and state machine
* Chef 10 - The Brain
* Straight DHCPD, no cobbler
* tftpd to deliver all sorts of images (Sledgehammer Discovery image, SUSE, Ubuntu, CentOS, RHEL, etc)
* nginx fronting repos of your favorite OS's packages and gems and whatevs
* Barclamps! which are units of Work in crowbar -- they are:
** Chef cookbooks
** Rails Engine implementing the crowbar_framework

Crowbar 1 - being demoed now

Crowbar 2 - 
* more sophisticated state model we call "annealing"
* Postgres as basis of store, not 100% reliant on chef

40-ish people working on Crowbar team at Dell

The admin node gets a little confused sometimes - race conditions, you can always run chef client again on it to fix up

1.x: Chef is used as the back end database.  Issues catching up with node changes when Chef is used as the back-end db.  Will change in Crowbar 2.

Running discovery image in RAM, can bring up a whole new rack of gear

In memory CentOS images run on nodes pulsing to announce node has been brought up - don't need hard drive installed in gear

"Allocate" - reboot node and apply BIOS settings, and install chosen OS.

aside: OpenStack SWIFT best to use JBOD not RAID

Dell provides (through your salesperson) Reference Architectures for Crowbar
* 720 server is bread and butter cloud gear box is most recommended
* 820 big beefy database boxes, not QAed by Dell.

OpenStack Ironic - does not do RAID and BIOS

Crowbar takes full control of IPMI - changes IPMI password
UEFI WSMan new metal standards for configuring BIOS

http://github.com/crowbar

Barclamp
* Whole lotta Chef and some bash
* barclamp-dell_raid - OPEN SOURCE!
* Partial Rails app RailsEngine
* Data bags get loaded to inform barclamp on how to work
* Databags for a bunch of expected network layouts

Neat thing about Network barclamp - will reorder NICs for you the way you like (despite what PCI bus thinks it should be)

How to customize OS install?  Use dev tool.  Can't assign kickstarts/preseeds per OS/MAC address, only by software stack

Need crowbar development environment

dev tool

Large shell script

Discovery image - sledgehammer

Pulls down image

Dev has commands to customize OS image among other things

Does it do Windows?  No, but deploying OpenStack with Hyper-V

Automatically deploys Ganglia and Nagios, NTP, etc.

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