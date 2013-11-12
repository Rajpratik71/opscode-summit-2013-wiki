What's Up with Berks 3?
=======================

## Conveners

Michael Ivy, Jamie Winsor, Seth Vargo

## Summary of Discussions 

Offial announcement - Opscode will take over ownership of Berkshelf.  Opscode will be stewards of Berkshelf, Riot will be involved of course

Answer questions about Berkshelf 3

Things to be excited about:
Will stop lying to you about resolution.  Since there is no authoritative place to make decisions about what cookbooks used can guess badly.  Now uses full graph of changes.  Requires API server now with a `universe.json` index of the community cookbooks.  Will need to run a Berks API server to index.

New community site will expose Berks API endpoint if you want to bundle the community site to do this

Berkshelf doesn't currently support indexing cookbooks.  Now with just a simple script you can update and re-index your own catalogue of cookbooks.

berks apply - takes resolve dependency tree applied as cookbook versions on an environment.  Get exact same versions in an environment - need this at Riot

Biggest complaint about Berkshelf
1) want results that don't lie
2) Fix the huge amount of dependencies for Berkshelf (actually ridley, but doesn't matter)

Biggest problem - dynamic dependency resolver - used to download dependencies, reflect on each - problem is dependency conflict.  Have to guess what version might be OK, and that's hard.  Build job can run for an hour backtracking.  Berkshelf was written because chef-librarian is slow like this.  Now Berkshelf lies ;-)

Solved with API server - application runs at api.berkshelf.com indexes cookbooks on github community site.  Looks at cookbook metadata publishing for anyone to consume.  No longer have to resolve these dependencies yourself.

Can merge results together from multiple API servers

Have tickets open for a local git server and a file system API server

Now you can stop asking us for nested Berksfiles

Not a presolved graph, it's a state graph of dependencies in JSON.  Download new state of the universe on each one.  Download massive JSON file.  Berkshelf still takes data and develops graph at runtime, it's not a pre-solved graph, but this improves the speed of the resolution.  It's slow currently on large Berskfiles because it's hitting a lot of repos that aren't cached.

Also similar to Bundler 1.5, can parallelize workers because we know everything we need to do up front.

Seth Vargo has been spearheading performance improvements.  Motherbrain - highly concurrent.  Ended up in ridley when it should have been separated out into gem.

Might notice commands like "help" and "version" take too long.  Will address performance of that.

Use Thor heavily for command line, considering dropping that because it uses reflection at runtime & that's slow.  Considering using Clamp - more object-oriented method and can pass loading options and lazy-load dependencies instead of having one huge Thorfile that is getting hard to maintain - like Ruby's autoload

Now when running "berks help" won't also load the installer.

What about Ruby autoloading?  Would like to use it.  Autoload if you define a constant as a symbol, ruby will search for symbol of that name to require that file to initialize a file.  Long thread on ruby forum that it's not thread safe.  Matz said it was dead in Ruby 3.  That being said Bundler uses autoloading.

We understand the performance issues with people running Berkshelf every day.  Multiple seconds to load the app is unacceptable.  Want to improve in Berkshelf 3.

And of course, will focus on overall bug fixes and improve error messages (stack traces/thread overflow from celluloid is unacceptable).  Don't expose to users.  For example, now you get a stack trace that the actor crashed when the chef server is unavailable.

Don't have release date yet.  You can use it now.  Jamie uses in it production everyday.
Can use `gem berkshelf install --pre`, but suggest using master branch

Will post instructions on how to use Berkshelf 3

Berkshelf will go into the Chef Omnibus installer - yay!  Better support tools like vagrant, delivering tools and making the experience better in getting started with Berkshelf.  Whatever feels good and what people want.

Triage meeting will be held weekly - don't know the time yet, but it won't be @ 1pm on Thursday as that's the worst time for the core committers.

What if I'm on an airplane and need the API?  Still have the lock file.  Will still honour the lock file.  If you haven't made any changes it will use it.  Don't touch your Berkshelf or lock file.

What if lock file says something different than the metadata?  Right now I delete my lock files all the time.  This is because Berkshelf currently lies to you, that should be fixed in Berkshelf 3.  (Technically not lying to you, but not noticing it because the version is not on the cleared list - we can hope that it works out or explode.  We chose to hope.)

Also keep in mind we didn't know Berkshelf would be useful ;-)  We didn't mean to open source it when we did, thus Berkshelf 3.

Would love to have more people working on Berkshelf.  Cache builder is an open ticket.

If we have private github cookbooks on hosted Chef, how are they indexed?  For internal github, Chef server is artifact server - pattern used is to sync github with Chef server with a CI latch.  Then have an internal Berks API server that indexes the Chef server.  Then it will merge and index the two sources.  Will have to run an API server locally if you are using Hosted Chef or Private Chef.  (There's a cookbook for it!)

`Berksefile` file example:

    SOURCE "BAPI.UNDEAD.NET"
    SOURCE "API.BERKS.COM"
    METADATA

API server has an endpoint to point at your github via the source attribute.  Order matters here.  Will grab from my local API endpoint first `BAPI.UNDEAD.NET`.  Can also still explicitly put git cookbook references in the `Berksfile` as well.

Should never have a request for nested Berksfiles again.

Without a dynamic cache builder, could generate a static file with a post commit latch.

Heroku could be used.

Declaration from Adam - we'll ship the api server in with Chef Server - so it will be done!

Why not have an Erlang API endpoint in the Chef Server?  That's probably what Adam meant.  Don't want to add more Ruby.  (Should have written Berkshelf in Exilir and call it a day).  It will sit in the Chef Server and it will be fine.

Does this change how I currently use Berkshelf?  No besides needing the API endpoint.

Will there be closer integration with knife?  Right now it's a pain to have to run `knife cookbook create` vs `berks cookbook create`.  Definite maybe.  Will standardize the dependency solvers and share codebase.  This integration should be better now that Opscode will be recommending Berkshelf as the recommended workflow.

Enhancement idea - sucks that `knife cookbook create` does not give you tests.

Perhaps need configurable template for cookbook creation options.  Ticket open on Berkshelf right now.  Should have templates in git to control berkshelf generate behaviour.  Person in Oregon will hopefully right this.

What about Windows support?  Mischa T. will help spearhead this.  Have more issues with Test Kitchen and Vagrant than with Berkshelf on Windows.  Opscode will be making Windows a first-class platform citizen with Chef over the next year.

## What will we do now?  What needs to happen next?

Start bundling the api endpoint into Chef.  Improve Windows support.