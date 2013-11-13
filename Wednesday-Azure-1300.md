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

`./bin/vagabond up`
`./bin/vagabond up cacher`

Idea is to get things up faster to get things working

With testing cookbooks it can be different to talk to other things.  Hard to configure `Vagrantfile` to configure multiple nodes.

Adds extra things to host node - an app cacher to build things locally

Can you interact with knife using vagabond?

Knife passthrough with vagabond - `./bin/vagabond knife cookbook list` - example
`./bin/vagabond knife node list`

End up building nodes then tearing them down again a lot.
`./bin/vagabond rebuild cacher`

Can do the same with clusters - goes through nodes serially in an array

Any way to build nodes in parallel?  Yes

Do you have to set a specific flag to build in parallel?  Yes `--parallel` flag, then it does everything in parallel

(Similar to vagrant)

`./bin/vagabond ssh cacher`

Minimalist for building nodes - nothing on them.  No users, you are root and that's what you get

Can send commands through as well

`./bin/vagabond ssh cacher 'ps -AH ux'`

Is there any advantage to using Docker?  Well it would be slower.

Can only run on Ubuntu/Debian, no LXC support in CentOS - Docker might be able to provide more support there, but I want to access LXC directly.

Philosophy is that you build chef from scratch then build node out

Based on LXC cookbook.  All structures used to build LXC containers can be specified in the Vagabondfile

No image shipping

Possible advantage to Docker, would build outside your workstation on structure - but basically re-building vagrant at that point

Do I need an external tool to validate the cluster?  Vagabond integrates with Test Kitchen and adds extra support for clusters to Test Kitchen

Did youtube video with Matt Ray on how this works
http://www.youtube.com/watch?v=FuarlNKs_FY&noredirect=1

How do you run cluster tests?  Passthrough to Test Kitchen
`./bin/vagabond kitchen`

Also supports [ServerSpec](http://serverspec.org) can run spec against the cluster in the `spec/` directory.  For a node, looks at the run_list, specs related to the node in the directory should pass

Serverspec is acceptance testing portion of Vagabond

`cat recipe/apt/cacher-ng/service.rb`

   require 'spec_helper'

   describe port(3142) do
     it{ should be_listening }
   end

`spec` block defines what we're doing - stuff to test clusters is kinda working.  End goal is to be able to properly mock everything in infrastructure.  Still need to finish.

Callbacks are supported - create, destroy, provision, whatever

Destroy good stand-in for garbage collection of nodes

Can use it now!

What about a template closer to my own environment?  The LXC container resource in the cookbook will let you do whatever you want, but I argue that you should provision that base to your final endpoint and don't change the base image - don't make assumptions that certain things are going to be there

Could use LXC cookbook to provision the host - to ensure things like wget or curl on the template

It actually downloads curl to install erchef

Example command to install Chef 10

    templates do
      ubuntu_1204_chef_10_26_0 do
        base 'ubuntu_1204'
        configuration do
          initialize_commands [
            'curl -# -L http://www.opscode.com/chef/install.sh | sudo bash -s -- -v 10.26.0'
          ]
        end
      end
    end

Is there something in there to test network partitions?  Like testing if something is unroutable?  Yes

Unwittingly used thor for command line, need to switch to mixlibs

Can set wait condition when things are finished when things are run in parallel?  For example, start running cookbooks when node has converged?  The Spec testing will do that - runs everything in parallel to create nodes, waits for that to finish, then runs the tests.

## What will we do now?  What needs to happen next?

Get Spec stuff finished

Get it to run against EC2, CloudStack, etc. instead of just LXC.  Use drivers from Test Kitchen (Sean Porter).  Make interface for Test Kitchen drivers to support this.

Look at making it also a small little daemon so the ruby bits always stay in memory and be faster - goal is to make it much faster - look at all the ways to make it go faster.

Hope to be able to mix and match EC2, CloudStack, Rackspace nodes together.