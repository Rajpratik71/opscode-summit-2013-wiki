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


