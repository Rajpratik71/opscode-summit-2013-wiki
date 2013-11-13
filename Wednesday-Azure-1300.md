Multi-Node Testing and Vagabond
===============================

## Convener

Chris Roberts

## Participants

## Summary of Discussions

https://github.com/chrisroberts/vagabond

Frustration with working with Chef servers very far away

Tried using vagrant at first working locally

Then tried writing bash script to provision nodes

Doing that for awhile, seemed a lot faster, so converted this to a proper tool

Been around for a little while

Under the hood uses an LXC cookbook to provision a system - a lot of state for it to work

Haven't been talking about it much because it's been changing frequently & used for personal projects

More proper release done the night before the comment summit

What it provides:

Runs off of LXC, initial provision takes a long time

Builds base templates for stuff being used (right now Ubuntu default)

Can specify templates

Takes initial base, converting it to some state, then snapshot the configuration and build templates out

After this initial slow run, everything else is really fast - all ephemeral nodes because it just sets up mount points on an overlay directory.  All changes are local (nothing saved elsewhere).  Easy to set up & tear down.

Two ways to run Chef Server with vagabond:
1) Erchef - Template with erchef to generate instances
2) Cher Zero - Better for low resource environments (erchef can be heavy)

`vagabondfile` describes what we have:

    Vagbondfile.describe do
      defaults do
        template 'ubuntu_1204'
        union 'aufs'
      end
      nodes.cacher.run_list %w(recipe[apt::cacher-ng])
      nodes.client.run_list %w(recipe[apt::cacher-client])
      clusters.cache %w(cacher client)
      server do
        zero true
        enabled true
        auto_upload true
      end
    end

Support for librarian & berkshelf

Vagabond file can be straight ruby hash - straight DSL to build Ruby hashes

Can specify a bunch of defaults, then override in other configs

We can do anything we can do with LXC - freeze nodes in a particular state, then thaw it out vs. needing to build stuff up then tear it back down.

Node is namespaces differently.

Very fast

`vagabond up`
`vagabond up cacher`

Idea is to get things up faster to get things working

With testing cookbooks it can be different to talk to other things.  Hard to configure `Vagrantfile` to configure multiple nodes.

## What will we do now?  What needs to happen next?