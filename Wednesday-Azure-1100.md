Continuous Integration/Continuous Delivery
==========================================

## Convener

Chris Wing

## Participants
jim (Thor) west
, ...

## Summary of Discussions

Spent past 6 months developing CI patterns.  Have spent most of my time managing Jenkins.

Different trains of development - based on pull requests

HP Cloud - OpenStack using Gerrit latch with Jenkins Job Builder plus JIRA tracking

Artifact pointers to cookbooks - everything versioned in Git and tagged with Git (need versioned data bags)

[Jenkins Job Builder](http://ci.openstack.org/jenkins-job-builder/)
Has dry run mode to test XML job that can be used before deploy

http://ci.openstack.org also good resource

Have super projects master branches pulling in sub projects - use Git as the verification mechanism

Problem pinning Jenkins versions - ever changing versions of plugins.  Solution - deploy Jenkins with Chef

Alternative to Jenkins?  [Thoughtworks Go](http://www.thoughtworks.com/products/go-continuous-delivery)

[Strider CD](https://github.com/Strider-CD) Nothing for programmatically adding jobs, but they are open to this.  Relatively new job.

Need DSL for build pipelines.  Cookbook promotions, artifact management.

State of Jenkins cookbook?  Ability to define pipeline?

What about running Jenkins on developer workstations?  Use buildbot - Chromium team has open sourced a bunch of things to support this workflow, developers run this on their machine: http://www.chromium.org/developers/testing/chromium-build-infrastructure/tour-of-the-chromium-buildbot

Manual quality gate or marketing gate still a problem.

JCloud plugin for Jenkins - should support hot slaves in the cloud -not ready for prime time

What about emergency patches?  External updates?  External updates should be just a matter of testing the app.  Perhaps consider "thou shalt not install from the interwebs".

fpm - used to bundle gems as an rpm - love fpm

## What will we do now?  What needs to happen next?