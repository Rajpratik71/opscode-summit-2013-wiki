Zap:: Pattern
=============
Cleaning up unused resources

## Convener
Joe Nuspl (nvwls)

## Participants

## Summary of Discussions
Example in http://github.com/nvwls/sysctl-cookbook
Working to open source a zap cookbook. Will announce on Chef mailing list when open.

How do we manage chef owned state. For example a cron job that is no longer needed or a sensu json? 
Dynamically create the all resources from data and templates and remove the rest.
Hooks to collect resources and hooks to remove what we do not create.

The alternative world view from puppet for managing directories. Perhaps it is a) too late to bring that mindset to chef and b) the cloud brings us all closer to immutable infrastructure. It may even catch up with the things we think today can only live in long lived nodes.

When and where to cleanup resources with examples of cookbook owned responsibilities and others were the responsibility can only be in the whole of the chef run. Then how do we make sure the cleanup knows what it need to know and occurs at the end of the chef run?

## What will we do now?  What needs to happen next?


