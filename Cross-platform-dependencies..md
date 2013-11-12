### (Potential) Issues that came up.

- Can makes cookbooks fragiles

- Test coverage increases exponentially

- Case statement complexity

- Attribute and library loading happens regardless if you use the cookbooks.

- Dependencies can be become a rats nest.

### Ways to make cross platform functionality more obvious and less complex?

- Moving cross platform functionality to providers may be more complex but cleaner.

- File standards in place of massive case statements.

- Write a client-side feature at the hack tomorrow to sanely include cookbooks for a platform.

Proposals 
- recipe level dependencies?
- lazy load recipes
- add supports syntax map
- - supports "windows", {depends: blah}