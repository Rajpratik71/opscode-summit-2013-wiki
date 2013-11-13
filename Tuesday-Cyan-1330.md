Chef and security
=============

## Convener
[Ilya Fomin](https://twitter.com/little_beat)
## Participants
Sean Nolen
Noah Kantrowitz
Rich Braun
Jon DeCamp
## Summary of Discussions

How can Chef help achieve/audit compliance?

Audit trail "activity logging": coming at some point from Opscode

One way to do compliance: pre-create AMIs with Chef, so that Chef doesn't even have access to prod


Even crappy processes can pass audits, but it's sometimes hard to change those processes (e.g. FDA requires you to prove that your new process is better than the previous one)


Ways to achieve security/compliance:
- Encrypted databags, but you still have to solve the problem of getting secrets to node  
  - Only works well if you want to be protected from your Chef server being compromized
- chef-vault is great, uses node public keys to encrypt attributes. BUT, you have to regenerate databag items whenever you add a node.
- With S3 security + IAM rules you can securely distribute secrets. Seems to work well.
- Enterprize Chef can do per-item RBAC.
- Openstack Barbican - still in early stages, looks promising


###Concerns:

- There are tools that can dump RSA signature from memory, so be careful and do panic!
- Passwords leaking in logs: might be a problem. Logging servers need to be most secure just in case.
- Secrets in Chef log: disable pretty error logging, send them somewhere, e.g. https://github.com/coderanger/chef-sentry-handler

###Conclusion:
- Don't use node attributes for passwords/secrets. Use resource attributes
- Make sure to secure file access to expanded templates
- If you just have to use passwords in node attributes: you can override node.save to not write those values to server. Still not a real solution.

- SOX is relatively easy to comply with, compared to HIPAA/PCI, because they don't force implementation on you

## What will we do now?  What needs to happen next?
- Spread the word and discourage using node attributes for passwords. MySQL cookboook needs to be fixed
- Introduce foodcritic rule to fail whenever node attributes are used for passwords/keys
 - Noah's recommending not to use node attributes at all
- At this moment, the only viable solution for dynamic environments is a 3rd party secret management tool
 - Relatively easy to implement. Just make sure to have tight security around it.
- For static environments, chef-vault works fairly well. Kudos Nordstrom guys!

