Session Title
=============

Chef 12, Versioning All the Things

## Convener

Matt Ray

## Vocal Participants

Dan Deleo
Stephen Lauck
Miah Johnson
Rich Braun
Nathan Zook
Matt Ray
MFV
Adam Jacob
Serdar Sutay
Seth Falcon
John Keiser

## Summary of Discussions

Versioning needs to be available for environments, roles and data bags to lock everything down for CI environments in Chef 12.

## Discussion Points

Use Git SHAs instead of versioning more artifacts?

How can we enforce automatic versioning of cookbooks? https://github.com/RiotGames/thor-scmversion

Lightweight feature branches are a must for deployment pipelines, changing the relation to Semver is important. Reality is that long-lived versioning should be detached from CI for sharing.

Today you can get versioning of artifacts by naming them with semver (roles, environments, data bags).

Semver is really important for community shared cookbook, less important in CI environments where the cookbook version is floating and auto-incremented as it flows through the system.

Chef Resources are not remembered between chef-client runs. The pain is that resources may have changed things previously but are unused. You can serialize the node and inspect.

## Environments ##

Should they be versioned since all they hold is versions? One alternative is to use a separate environment for everything.

Is the Git SHA good enough? Environments should track all the versions of everything.

Environment is a place for policy for defining which artifacts the Chef server will give you. Environments are a set of nodes.

CI environments have a need for versioning. Behavior would be unchanged if versioning follows HEAD unless otherwise set.

## Roles ##

Solution to wrapper cookbooks? Useful for versioning in CI environments.

Environment specific run lists are bad.

## Data bags ##

Stand-alone JSONs, files can be versioned, but should Chef do anything about that?

## Attributes ##

Chef attribute set tracing is CHEF-2913

## Potential Code cleanups ##

How do we get seen recipes and roles in a consistent, coherent fashion?

Policy enforcement to pin all cookbook versions, block all cookbooks not listed in the environment. Cookbook whitelist for the Chef server.

Freezing cookbooks by default? Force-freezing of everything could be a feature for config of the Chef server.

Garbage collection of old revisions by policy would be nice, remove unused old artifacts.

Platform specific dependencies in metadata for cookbooks.

Honor 'provides' from cookbook metadata for dependencies.
