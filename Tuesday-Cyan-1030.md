Chef without a git repo
=======================

## Convener

Jaime Winsor

## Participants

Not recorded.

## Summary of Discussions

(these are raw notes from the session)

Berkshelf get rid of repo of submodule of things. At the time chef
repo cookbook environments roles and data bags in it. First thing we
did was idea that cookbooks live there. Instead, each cookbook has own
repo and build job. And CI to drive that. Then started working on
orchestration (motherbrain at riot). What you're doing is changing the
data on the chef server and having the nodes check-in. If you have a
tool that manipulates the chef server and you also store all the data
in a git repo, then those get out of sync. If anybody pushes, you lose
the update from the orchestration tool.

To upgrade an app, change a node attr to deploy 2.0. But with an
environment file it would override the changes of the orchestrator. So
removed environment files. Roles didn't ever get used (not versioned
and no place in setup). Data bags was last thing. A lot were
encrypted. So what's left in this repository? Maybe a berksfile (I
don't particularly do that). Every cookbook should have its own
job. They have a build job together. Disagreements between source of
truth github vs Chef Server.

I've worked with software before and then I've hated it. BUt 

Doug I: our philosophy is everything should come from git and git is the source of truth.
Which nodes go to which environments.

We have a problem where devs don't push or don't commit.

We have a jenkins job that uploads cookbooks to server after tests.

You shouldn't be using knife every day.

If only there was this Chef Jenkins thing that would do it all for us?

DougI: restaurant you push to git and that triggers jenkins job does
linting, updates equality pinning. Enforces that all changes have to
be code reviewed and tested. Will likely be open sources for CD
pipeline. Atlassian stash as git server. We have a repo per
cookbook. Pipeline is all cookbook driven. It also works
multi-org. Pushes to multi orgs. You push up to the repo in stash and
then stash has rules that enforce rules.

Seth: flat cookbook group gives uou git grep. 

The chef cookbook indeer is a good diea Rackspace deployment
services. We've given them the say of using berkshelf and
everything. There is this repo of random cookbooks. We have to go find
the bomb on a fresh set of cookbookjs. So an indexer would be
perfect. And it would be simple to. How many resources. You can
compile the cookbook and reflect on the content.

Adam: started using berkshelf's local install. Give me all the junk in a directory.

The resource collection once you've done the compile phase. So a
really easy way is take the resource collection in a post converge
handler and put it into solr.

Jaime: just grep the cookbook store in ~/.berkshelf/cookbooks.  So
also "berks ack". Introspection tool on the node. Checks it's cookbook
dir and its runlist and tells you the things it converged
on. Profiling tool.

Did you guys ever read a book called continuous delivery? A little
repetitive. The idea that you should deliver software to your customer
as fast and as often as possible. The delta between changes expect
minimum time to identify problems.

Jaime: Why I don't have this problem.

    git
       app
       cook
    
Jenkins using TestKitchen and maybe ChefSpec

1. App
2. cook


So cookbook job:

1. checkout
2. test
3. bump version
4. publish


app job:

1. checkout
2. build
3. unit test
4. package, release
5. deploy to dev
6. functional test


another job for staging. Taking the artifact. 

staging: deploy, functional test, perf test

Matt: I did this and people were like meh

Jaime: you give the biz a lever to deliver quickly.
The last mile to get to prod is the orchestration part.

So what goes into this are the wrapper cookbooks and you have to
manage those as well. So you do get some explosion of count of
cookbook repos.

Monitoring needs to be integrated into app cookbook. Perhaps with an
infrastructure wide base cookbook that provides LWRPs. So a libary
cookbook and then you have a recipe in every application cookbook
that's called monitoring. And ties it together.

I wish it was in text files that I could represent. And if bamboo dies
-- all these jobs are GONE.

Q: How do you differentiate between major and minor cookbook changes
Gets bumped by hand when someone does a big refactor. Pretty much an
app cookbook doesn't change so no breaking API.

Lamont: I have 60 cookbooks. So feels like there's something
missing. Want vendored or raw clone it all, not just download/copy.

## What will we do now?  What needs to happen next?

1. Consider adding a `berks grep` command

