Build Systems
=============

## Convener

Rich @Splunk

## Participants

## Summary of Discussions

Built web site from scratch, @Gap adopted Jenkins, using it to build systems and develop software

@Splunk have to recreate the build server environments repeatedly

Two different approaches to defining tools:

* Central place to work for builds
* I want to build isolated on an airplane

How to integrate the two

Repo servers and proxying - how to get Splunk servers building in your environment, for example.  Containerize how to get Jenkins and so forth, like pypy & gems.

Security

Innovation in my current job - Create a single object defining a whole stack - different roles of spunk machines.  Plus add build rules.

Documentation

Promotion rules - QA team cutting release, manual steps for ops team to deploy.

Went down Jenkins route - bolting the CD concept on existing CI systems is a common approach, but doesn't work.  Death to Jenkins!  Think of systems as end-to-end pipelines.  Build + Deployment, not just build.

Would like to definite two or three standard pipelines for all kinds of software.

Why do I need to Chef the build system?  After yet another upgrade the JIRA system, the thing went down for an hour and nobody could use it.  If I don't put my build system through the same kind of discipline as the rest of the production system, I'm setting my company up for failure.

Build jobs should not codify the pipeline.  Instead the CI/CD system codifies the pipeline.

In the tool writing at Opscode, build scripts live in source control, scripts don't live in central server

Been working on this project for two months at Opscode.  Would like it to be available next August.

Assumes that Pushy is a great job description framework

Is very prescriptive about the pipeline

Specify build cookbook that maps to each of the phases, then run the build

What if I need to run on three different environments, parallel provision them as quickly as possible?  There is a provision phase.  It is constrained in what those environments are.  There are four different environments.  But in that you can define what you want to accept in the environment.

Build cookbooks are the language of the build.  What if you could write a cookbook to define a Java build?  We've proven if we can do that?

Intention is that this defines how you define software development and backing the community site.

How do you help you along the way?  We need to work that out?



## What will we do now?  What needs to happen next?

Go back to Opscode to provide a build service for the community to collectively improve