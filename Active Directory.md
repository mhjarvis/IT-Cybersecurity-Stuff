# <h1 style="text-align:center">Active Directory</h1>

## Introduction
To help manage large Windows-based netwroks (e.g. configure policies, provide on-site support), we can use a Windows domain. A Windows domain is a group of users and computers under the administration of a business / org. The main idea behind such a domain is to centralize the administration of the common components of a Windows computer netwrok in a single repository called Active Directory (AD). The server running the Active Directory services is called the Domain Controller (DC). This provides:

* Centralized identity management
* Managing security policies

A common example of AD in use is on a college campus where you can log into the school org with a username/password, but you have restricted access to numerous functions (e.g control panel). 

The core of any Windows Domain is the Active Directory Domain Service (AD DS), which is a catalogue that holds information of all objects on a network, such as:

* Users - an object known as a security principal (it can be authenticated by the domain and can be assigned privelages over resources). Users are used to represent people (persons in your organization) and services (every service requires a user to run, but these are different from regular users). 

* Machines - another type of object; for every computer that joins the AD domain, a machine object is created. These are also considered 'security principals' and are assigned accounts like regular users. Machine accounts follow a naming scheme - the computers name followed by a dollar sign ```DC01$```.

* Security Groups - allows you to assign privelages to a set of users, machines, or other groups. Some example of the more important groups in a domain:
    
    * Domain Admins - have admin privilegas over the entire domain (can administer any computer on the domain).
    * Server Operators - can admin Domain Controllers; they cannot change any admin group memberships.
    * Backup Operators - users in this group can access any file, ignoring permissions. Perform backups of data.
    * Account Operators - users in this group can create/modify other accounts in the domain.
    * Domain Users - includes all existing user accounts in the domain.
    * Domain Computers - includes all existing computers in the domain.
    * Domain Controllers - includes all existing DCs on the domain.

* Organizational Units - container objects that allow you to classify user and machines. They are used to define sets of users with similar policing requirements. 