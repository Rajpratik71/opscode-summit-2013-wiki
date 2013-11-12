Cookbook / ICLA Site
=============

## Convener
[Bryan McLellan](https://twitter.com/btmspox)

## Participants [and people that btm saw]
[Seth Vargo](https://twitter.com/sethvargo)  
[Sean O'Meara](https://twitter.com/someara)  
Nathan Smith  
[Noah Kantrowitz](https://twitter.com/kantrn)  
[Miah Johnson](https://twitter.com/miah_)  
[Tim Dysinger](https://twitter.com/dysinger)  
[Ian Meyer](https://twitter.com/ianmeyer)  
[Nathen Harvey](https://twitter.com/nathenharvey)  
Stephen Lauck  
[Steven Danna](https://twitter.com/SteveDanna)  
[Stephen Delano](https://twitter.com/sdelano)  
[Joshua Timberman](https://twitter.com/jtimberman)  
Jon Ong  
[Pauly Comtois](https://twitter.com/paulycomtois)  
[Sascha Bates](https://twitter.com/sascha_d)  
[Scott Christopherson](https://twitter.com/Scottopherson)  
[Seth Chisamore](https://twitter.com/schisamo)  
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