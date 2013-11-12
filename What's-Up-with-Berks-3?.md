What's Up with Berks 3?

Michael Ivy, Jamie Winsor, Seth Vargo

Offial announcement - Opscode will take over ownership of Berkshelf.  Opscode will be stewards of Berkshelf, Riot will be involved of course

Answer questions about Berkshelf 3

Things to be excited about:
Will stop lying to you about resolution.  Since there is no authoritative place to make decisions about what cookbooks used can guess badly.  Now uses full graph of changes.  Requires API server now with a universe JSON index of the community cookbooks.  Will need to run a Berks API server to index.

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
