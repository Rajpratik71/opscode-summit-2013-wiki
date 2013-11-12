### If it's infrastructure as code, why don't we write it like the rest of our software?
#### Jeff Smith - [Rally Software](http://github.com/RallySoftware-cookbooks)
#### Participants

#### Summary of Discussions
Jeff - Overview of the problems we face @rally - TDD, pushing cookbooks to hosted chef with each commit.

* What does TDD mean to us? Writing a failing test first.
* Using test kitchen for wiring tests, and chef spec as unit testing.
* At what level do you unit test a cookbook? - Try to unit test the logic not the declarations. 
* We are not all coders needs to be changed. Because of chef we all need to be coders.
* Team make up - How does team make up affect the IAC? 
* Agile has been fighting TDD for years and we should be embracing that discussion as well. 
* Chef Spec - What type of logic? - URL to zookeeper is one (if you have multiple clusters). 
* State of testing continues to evolve! - Current state of cookbook testing, foodcritic, chefspec, test-kitchen (serverspec/bats). Testing chef outside of chef.
* Chef as a schema-less design. What happens if a databag is in the wrong structure? Comes down to who can actually write to the chef server. 
* Continuous delivery toolset - jenkins is the only that should write to hosted chef and version cookbooks.
* timestamps as major, minor, patch SCM version.
* each cookbook gets its own acceptance or dev environment and when you promote everyone updates that dependency.
* rolling back is really hard. Maybe just 1 version rollback. 
* rolling forward vs fighting forward
* what is the artifact at the end of a CI pipeline? cut an image?
* roles - collection of attributes. Just make a cookbook (application cookbook). 
* how you introduce a community cookbook into a controlled environment? - Wrapper cookbook with tests? 
* Community cookbooks with tests? Not many? 
* Running tests before each commit - Guard, precommit hooks, lights, etc...
* travis w/ test kitchen - use AWS as in between.
* cookbook generation with scaffolding
* unit testing LWRPs is hard - writing ruby classes and using rspec is one way to do this. (talk about @130)
* just enough ruby for chef? probably not a reality. ruby is core to chef and you should be learning ruby to make your cookbooks better.
* teaching testing should be an entry level item

#### What will we do now?  What needs to happen next?
* Just enough software engineering for chef? 
* knife cookbook create should help create scaffolding (templatized/configurable)
* CI system for community cookbooks
