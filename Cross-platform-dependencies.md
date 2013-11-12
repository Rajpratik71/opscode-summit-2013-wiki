### Convener

[Ian Coffey](http://github.com/iancoffey)

### (Potential) Issues that came up.

- Including non-essential cookbooks can make render the run fragile

- Test coverage increases exponentially

- Huge case statements grow complexity and decrease readability. 

- Attribute and library loading happens regardless if you use the cookbooks.

- Dependencies can be become a rats nest.

### Ways to make cross platform functionality more obvious and less complex?

- File standards in place of massive case statements.

- Extend cookbook dependencies

### Proposal
- For the in-recipe stuff, file path attributes could become more of an accepted standard.
- For actual cookbook dependencies, submit a pr introducing conditionals on "supports"
eg. supports "windows", {depends: blah}