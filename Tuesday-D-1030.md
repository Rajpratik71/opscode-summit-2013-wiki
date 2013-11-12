Cookbook / ICLA Site
=============

## Convener
Bryan McLellan

## Participants [and people that btm saw]
Seth Vargo  
Sean O'Meara  
Nathan Smith  
Noah Kantrowitz  
Miah Johnson  
Tim Dysinger  
Ian Meyer  
Nathen Harvey  
Stephen Lauck  
Steven Danna  
Stephen Delano  
Joshua Timberman  
Jon Ong  
Pauly Comtois  
Sascha Bates  
Scott Christopherson  
Seth Chisamore  
Sean Horn   
Cary Penniman  
lots more...  

## Summary of Discussions
[Supermarket](https://github.com/opscode/supermarket) - New project repository.

How to contribute
 - Sign a CLA
 - Join the chef-dev mailing list
 - Open pull request

### Namespacing
One cookbook that solves all use cases on all platforms isn't possible.

Namespacing design options
  - Separate string
    - Not used internally by Chef
    - Not part of dependency resolution
    - Part of the cookbook metadata
  - specific delimiter (bob/apache2)
    - by community user
  - Unique identifier / hash / UUID
  - Alias for the cookbook
    - 

Cookbook metadata versus external tools, e.g. Berkshelf

Is the namespace the problem?
  - Fix our cookbooks first, then namespacing
  - Who blesses the one good cookbook?
  - How do you promote an alternative better cookbook?
  - How to depend on a specific 'mysql' cookbook?
  - Rubygems has no namespacing
    - Encourages creative naming

### Site Features

How to measure cookbooks?
  - Is this the right cookbook for me?
  - Objective
  - Subjective
  - Download counts
  - Voting
    - Beginner cookbook? Level of experience needed?
    - Used in production
    - Karma system
    - Bad dependencies affect score
  - Ruby toolbox
    - Code climate
    - Required/Optional testing
    - Metascore

Testing
  - Green/Red flags
  - test-kitchen?
  - Travis?
  - What infrastucture will Opscode provide?

## What will we do now?  What needs to happen next?