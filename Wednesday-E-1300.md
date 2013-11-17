Tooling choices discussion
==========================

## Convener

## Participants

## Summary of Discussions

Tooling choices talk
--------


Things that make writing awesome:
----
- Access to docs Built into tools
- A text editor
- Autocompletion
- Syntax checking / hilighting
- Inline linting
- Built/test integration (guard / tmux / IDE's like Eclipse || foodcritic / rubocop / chefspec)
- Integration with reporting ( )
- 3-way diff of central vs. local vs. knife-diff
- Get rid of housekeeping - metadata.rb maintenance, etc.
- Code generators need to be more awesomer (templatized, extensible, feature switches, etc.)

A wild Omnibus discussion appeared! It's sort of effective!
----
- We need more education around Omnibus.
- Should we bundle a bunch more tools into chef-omnibus?
	YES
	YES WE SHOULD
- People like Omnibus use cases.

The discussion jumps to the Test phase
----
- Charles presents the usual signal in / signal proc / signal out discussion
- All the post-run test inspections are flawed in some way
	- Serverspec has to re-implement system profiler
	- BATS is bash (fuck bash)
	- Minitest has no sugar, have to write it all ourselves
	- Chef-minitest-handler is married to the chef-client run
- Dissent! Worries about beginners mutating state in spec.



## What will we do now?  What needs to happen next?

