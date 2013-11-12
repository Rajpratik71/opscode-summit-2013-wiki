### (Potential) Issues that came up.

- Including non-essential cookbooks can make render the run fragile

- Test coverage increases exponentially

- Huge case statements complexity and decrease readability. 

- Attribute and library loading happens regardless if you use the cookbooks.

- Dependencies can be become a rats nest.

### Ways to make cross platform functionality more obvious and less complex?

- Moving cross platform functionality to providers may be more complex but cleaner.

- File standards in place of massive case statements.

- Write a client-side feature at the hack tomorrow to sanely include cookbooks for a platform.

Proposals 
- file path attrs more of a social standard
- cookbook depends conditionals
- - supports "windows", {depends: blah}