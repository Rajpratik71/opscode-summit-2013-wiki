Continuous Integration/Continuous Delivery
==========================================

## Convener

Chris Wing

## Participants

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

## What will we do now?  What needs to happen next?
