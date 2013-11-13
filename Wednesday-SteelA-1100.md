Rethinking Search
=================

Attendees
---------
Seth Falcon (host), Dan DeLeo, Jamie Winsor, Cary Penniman, Others

Overview
--------
Search needs scaling fixes

###  Two Main Use Cases
 1. AdHoc Infrastructure queries and questions (don't necessarily need to be fast)
 2. Environment workflow/automation/coordination (needs to be fast!)

Current Pain Points
-------------------
 * Scaling out
  * Latency from index update to query-able (can be 1 min+)
  * Latency of search query : averages are okay, the maximums are not.
  * Latency of index update
 * Client Side
  * Performing search before saving node : results will possibly not contain the current node.
  * Searching across chef servers is not supported
    * is possible, but not part of DSL (Winsor)
 * Shifting node data structure can break queries over time.
 * Not able to wait for specific search criteria to be true
  * useful for blocking script execution (for example, having an app server wait for a DB to be available)


Requirements
------------
Some things we need search to do:
 * exact matches
 * wildcard matches
 * range matching (might be nice)

Ideas/Suggestions
-----------------
 * Investigate Sphynx search engine (out of russia)
 * What if node.save() was slower, so that it is query-able faster? (Seth)
  * Consensus is that this is a good trade off.
 * Also support "faceting" or grouping of result set 
  * opinions were that this could be implemented in the UI or App Layer
 * Have server return token so one can wait for async event
 * Add a "bulk" databag API support
 * Define "Fast" queries as separate API calls. (Winsor)
 * You must search for both "recipe:app1" and "recipe:app1::default" (Winsor)
  * writing this should just append "::default" if not there
 * Bad stacktrace from a search failure -- not user friendly. (Winsor)
  * allow defining error messages, on_error callback and/or default return values in the search DSL.

Other Stuff
===========
 * partial search cookbook available https://github.com/opscode-cookbooks/partial_search
  * needs tests! -- volunteers?
 * Cary's working on a machine_tag cookbook to avoid the changing node data structure issue
  * needs contribution for Chef Server support (using partial search)
  * https://github.com/rightscale-cookbooks/machine_tag
