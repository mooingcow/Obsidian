--- 

## Active Directory (AD) 
--- 
- Essentially a database to provide centralised control and storage (passwords, Group Policies)
- Stores resources (Printers/Share Folders)
- Services like Email uses AD
- Stores Group Policy settings (make centralised changes to network quickly and easily )
- Everything in AD is an object

###### Workgoup
- Every computer on the network has it's own small database of usernames 
- No central control
- To login to a new computer, a new user account and password needs to be created
- Problems: 
	- 1. Does not scale well - each time a change is made, all computers affected by the change must be manually configured
	- 2. User accounts and passwords not synced between computers

###### Domains
- Logical group that shares the same AD database
- Share the same namespace

###### Domain Controller (DC)
-  Runs Active Directory Domain Services (a role!)
- Holds a copy of the AD database
- Replicates changes with the DCs throughout the network
- To keep AD database up to date 
- Authenticate users to allow them access to the network
	- Determines access of each user

###### Forest vs Tree vs Domain
##### Parent & Child Domain
- 
- As long as they share the same root namespace, they can be added to the original domain as a child domain. 
- they are in the **same tree** 