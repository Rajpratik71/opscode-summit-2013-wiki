Making Chef on Windows Better
=============

## Convener(s)
Kristian Vlaaderingbroek (Schuberg Philis)
Garrick Olson (Pariveda Solutions)

## Participants -- please add yourself!
Jeff Mendoza (Microsoft Open Tech)
Julian Dunn (Opscode)
Alex Vinyar (Opscode)
Makana Greenwell (Opscode)
Ken Cheney (Opscode)
Brian Scott (Disney)
Mark Mzyk (Opscode)
Jon DeCamp (Nordstrom)
Jeff Hagadorn (Disney)

## Summary of Discussions

* General impressions of Chef on Windows
  * Feels "gimped" compared to Linux
    * Thing that work on Linux often don't work the same way on Windows
    * Being a Chef expert on Linux doesn't help you avoid starting all over when moving to Windows
    * Have to install lots of 3rd party tools (e.g. ssh, openssl, Cygwin) to use Chef / knife effectively
  * Using knife workstation requires a ton of setup to get productive -- e.g. install git, install editor, etc.

* Pain points:
  * Remote WinRM execution of chef-client
    * Fails for things like SQL Server because of WinRM's restricted token
    * Workaround is to create a remote task
    * RunAs and ElevateMe may work around this
    * Better way to do this -- use Pushy!
      * Pushy lets you reach out and run a command, e.g. Chef-client, with full privileges
      * Pushy has analogs in MCollective, Salt, etc.
    * Another possible fix:
      * Utilize existing Windows Service with a new feature where it can be "tickled" to run chef-client with full privileges   
  * Bootstrapping not as reliable as Unix
      * Too many hoops to configure WinRM or ssh
  * Knife workstation::
      * (Some) Windows admins may need a GUI!
      * Extra work after you install chef msi to install / configure editor, git, etc.
        * Common editors: notepad++ (approved by many IT depts), RubyMine, Sublime
      * Slowness in Ruby
  * Chef-client
      * I always need the Windows cookbook -- put resources in core Chef!
      * I always have to shell out to Powershell -- need more resources or Windows-specific primitives (i.e. resources) -- see list of problem scenarios

## What will we do now?  What needs to happen next?

* We need to generate more Windows content
  * Ask Opscode for commit access for your favorite cookbook / prospective cookbook
  * Add your cookbook requests to the end of this document, nice if you link it to a COOK ticket in https://tickets.opscode.com
* We need to come up with a prescriptive knife workstation for Windows -- and AUTOMATE IT!
  * Add knife windows workstation setup to the Windows MSI (or a special MSI)
    * This would include things like the editor, git installation, etc.
  * Everyone: add your ultimate Windows knife workstation configuration to the end of this document
* We need to fix WinRM
  * Needs to work with stock Windows images -- Windows VM images require lots of hacking to work with bootstrap / Chef compared to Linux
  * Needs to work with Negotiate protocol and SSL endpoints
     * Is an ssh-like workflow for winrm access useful?
  * Current WinRM security limitations mean it won't be allowed by many organizational policies
  * SSH is not part of Windows and may thus violate other organizational policies
* Get Microsoft as part of the community!
  * MS Open Tech contributes to open source projects -- how about contributing to Chef and cookbooks?
* Add rest of Windows cookbook resources to core chef
* Implement PowerShell DSC cookbook!
* Try out latest update of knife-windows to see how Windows bootstrap reliability / logging improvements can be extended further
  
## Your Windows specific scenarios that need help -- add them here:

* Missing cookbook content
  * WSUS Server setup / configuration
  * Exchange Server setup
  * IIS
  * Active Directory cookbook needs to be rewritten
  * Domain join
* Chef-client execution contexts
  * Remote execution of chef-client on-demand
  * Use of domain credentials -- needed to access domain resources
* Building VM images via Chef
* Missing primitives -- many of these require shelling out to Powershell to work around lack of primitives
  * Group Policy Management
  * Patch Management -- use Chef to approve and configure patches on the node
  * IIS config
  * File share management
  * Windows impersonation
  * Powershell DSC


## Your knife Windows workstation config
 
* Example: Emacs + ConEmu + git + chocolatey (http://chocolatey.org)


