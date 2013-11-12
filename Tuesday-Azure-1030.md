Introduction to Crowbar
=======================

## Convener

## Participants

## Summary of Discussions
What is crowbar?
Two and a half years ago colleagues tried to install
OpenStack.  Hellish to install OpenStack.  Gear still in boxes
nothing was going on.

Crowbar focused on bringing up near gear

Straight DHCPD, no cobbler

Crowbar 1

Crowbar 2 - more sophisticated state model

46 people working on Crowbar team at Dell

Admin node

TFPD server - straight

Run chef client again to fix up

Chef is used as the back end database.  Issues catching up with node changes when Chef is used as the back-end db.  Will change in Crowbar 2.

Crowbar 2 - Postgres database & Chef 11

Crowbar 1 - Chef is database & Chef 10

Running discovery image in RAM, can bring up a whole new rack of gear

In memory CentOS images

Allocate - reboot node and apply BIOS settings

OpenStack SWIFT best to use JBOD not RAID

Reference architecture

720 bread and butter cloud gear

820 big beefy database boxes

Ironic - does not do RAID and BIOS

Ironic allocate bare metal

Full control of IPMI - changes IPMI password

UFI WSMAN new metal standards for configuring BIOS

github.com/crowbar

Barclamp

Whole lotaa Chef and some bash

barclamp-dell_raid

Partial Rails app RailsEngine

Data bags get aloaded to inform barclamp on how to do it

Databags for a bunch of expected drive layouts

Neat thing about BIOS barclamp - will reorder NICs for you (despite what PCI bus thinks it should be)

How to customize OS install?

Need crowbar development environment

dev tool

Large shell script

Discovery image - sledgehammer

Pulls down image

Dev has commands on

Does it do Windows?  No, but deploying OpenStack with Hyper-V

Automatically deploys Ganglia

Does it scale?  Crowbar backs off when you try to scale horizontally

Crowbar is a bar clamp of itself

## What will we do now?  What needs to happen next?
