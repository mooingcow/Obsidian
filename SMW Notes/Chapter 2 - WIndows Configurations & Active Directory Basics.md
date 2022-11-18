--- 

## Server Roles
---
Common Roles:
- File and Storage Services
	- Allow sharing files from the server
	- Using the server to coordinate and simplify file sharing through Distributed FIle System (DFS)
- Print and Document Services
	- Manage network printing services
	- Offer one or more network printers connected to the network through the server itself
---

## Best Practice Analyser (BPA)
---
- Run BPA to determine if one or more roles are installed and configured to follow guidelines recommended by Microsoft
- Three levels of severity to each problem found:
	- Information 
	- Warning
	- Error
- Guidelines used for analysis
	- Configuration
	- Security
	- Predeployment
	- Postdeployment
	- Performance
	- BPA Prerequisites
---

## System File Checker
---
- Scan system files for integrity
- Scan and replace system files as needed
- Run from Command Prompt or Windows PowerShell (requires admin right)
	- sfc/scannow
---

## Sigverif
---
- Verifies system and critical files to determine if they have a signature
	- Only scans files and does not overwrite inappropriate files 
		- Can be used while other users are logged on
- Results output to a log file --> sigverif.txt
- Files can be replaced when users are off the system
---

## Windows Server Reigstry
---
- Contains all the information a system needs about the entire server
	- Coordinating center for a server
- Contains data about:
	- Hardware components
	- Windows Server services that are installed
	- User profiles and group policies
	- Last current and last known setup used to boot the computer
	- Configuration information about all software in use
	- Software licensing information
	- Server manager and Control Panel parameter configurations
- Registry Editor launched using --> regedit
- Precautions:
	- Only specific group of admins should have priviledges to open and modify the registry 
	- Only make changes to the registry as a last resort
	- Regulary back up the registry as part of backing up the Windows Server Windows folder
	- Never copy the registry from one Windows-based system to the registry of another system

###### Registry Contents
- Hierachical in structure --> contains keys, subkeys, and entries
- Keys:
	- Category of division of information within the Registry
- Subkeys:
	- Single key may contain one or more lower-level keys
- Hive:
	- A set of subkeys stored together because they hold related information
- Entry:
	- Data parameter associated with a software or hardware characterisic under a key (or subkey)
- Root Key:
	- A primary or highest level category of data contained in the Registry
	- Total of 5 Root Keys:
		- HKEY_LOCAL_MACHINE
			- Contains information on every hardware component in the server
			- Includes information about what drivers are loaded and their version levels, setup configurations, BIOS versions, and more
		- HKEY_CURRENT_USER
			- Contains information about the desktop setup for the account presently signed in to the server console
			- Alias for HKEY_USERS\\logged-on user hive
		- HKEY_USERS
			- Contains profile information for each user who **has** logged onto the computer
			- Each profile is listed under this root key 
			- Information is identical to that viewed within HKEY_CURRENT_USER root key
				- Profile user when signed in is one of the profiles stored under HKEY_USERS
		- HKEY_CLASSES_ROOT
			- Hold data to associate file extensions with programs
			- Alias for HKEY_LOCAL_MACHINE\\Software\\Classes
			- Associations exist for executable file, text files, graphical files, clipboard files, audio files, and more
		- HKEY_CURRENT_CONFIG
			- Holds information about the current hardware profile 
				- Monitor type, keyboard, mouse, and other hardware characteristics for current profile

###### Backing up the Registry
- To create a backup --> set a restore point 
	- Use Checkpoint-Computer cmdlet in PowerShell
- If registry is damaged, go back to the restore point

## Active Directory (AD) 
--- 
- A database to provide centralised control and storage (passwords, Group Policies)
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
- Replicates changes with the DCs throughout the network to keep AD database up to date 
	---> Multimaster Replication
	- To make replication more efficient:
		- Replicate individual properties instead of entire accounts
		- Replicate AD on the basis of speed of network link
- Authenticate users to allow them access to the network
	- Determines access of each user
- **Special DC** --> Bridghead Server ^e7d681
	- Has the role of exchanging replication information

###### Forest vs Tree vs Domain
##### Trees
- Domains sharing the same root namespace with parent and child domains
- As long as they share the same root namespace (contiguous namespace), they can be added to the original domain as a child domain (e.g. Parent: ITFreeTraining.com; Child: Secure.ITFreeTraining.com)
	- They are in the **same tree** in AD
		- e.g. ITFreeTraining.com is at the top of the tree, so it is the root domain
		- e.g. Adding another domain, Sales.ITFreeTraining.com, is part of the tree as it shares the ITFreeTraining.com namespace 
- Each domain has its own AD database
- AD automatically create trusts between parent and child domains 
	- Allow members of each domain to access resources in any other domain **ASSUMING** they have access
##### Forest
- Encases multiple domains and trees
- As long as there is 1 domain, a forest is automatically created
	- Adding child domains to the root domain creates a tree within the forest
	- Adding another domain with a different root namespace creates another tree in the same forest (disjointed namespace)
- All domains in a forest share the same **schema** 
	- Defines objects and attributes of objects in the AD database 
	- Shared between all domains in the forest
	- When changes are made to the schema, it is replicated to all domains in the forest
AD automatically create trusts between trees in a forest 
	- Allow members of each domain to access resources in any other domain **ASSUMING** they have access
##### Global Catalog Server
- Stores information about every object in the forest
- First DC configured in a forest becomes the GC server
	- At least one GC per domain
- Store a full replica of every object in its domain, and partial replica of each object within every other domain in the forest
	- Enables forest-wide searches of data
##### Multiple Forests 
- Each forest has its own AD infrastructure
- Administrator must manually create a trust between forests
- Each forest has its own schema, and each domain has its own copy of the AD database

###### Organisational Unit (OU)
- A grouping of related objects within a domain
- Achieve more flexibility in managing resources associated with a business unit, department, or division
- OUs can be nested within OUs

###### Site
- TCP/IP based container within AD that is linked to IP subnets
- Based on connectivity and replication functions
- Functions:
	- Reflects one or more interconnected subnets
	- Reflects the physical aspect of the network
	- Used for DC replication
	- Used to enable a client to access the physically closest DC
	- Composed of only servers and configuration objects
- Reasons for defining a site:
	- Enables a client to access network servers using the most efficient physical route
	- DC replication is most efficient when AD has information about the locations of DCs
	- Sets up redundant paths between DCs
		- Paths used for replication
- Only one [[Chapter 2 - WIndows Configurations & Active Directory Basics#^e7d681|bridgehead server]] should be set up per site

###### Guidelines 
- Implement least number of domains possible --> 1 domain is best
- Use OUs to reflect organisation's structure 
	- Windows prefer OUs set up horizontally instead of vertically
	- No more than 10 levels of OUs
- Use domains as partitions in forests to:
	- Demarcate commonly associated accounts and resources
	- Governed by group and security policies
- Use sites to improve logon and DC replication performance
	- When there are multiple IP subnets and multiple geographic locations 
---

## Security Configuration Wizard (SCW)
---
- Analyses and configures security settings on a server 
- SCW examines the roles the server plays
	- Tries to adjust security settings to match these roles 
	- Unlike BPA, SCW allows the administrator the choice of applying the change immediately or not
- Functions:
	- Disable unnecessary services and software
	- Close network communication ports and other communication resources that aren't in use
	- Examine shared files and folders to help manage network access through access protocols
	- Configure audit policy
- 3 components:
	- GUI interactive wizard
	- Database
	- Command-line tool --> scwcmd
- Security Configuration Database (SCD)
	- A group of XML files that establish a security policy


###### Kwan
1. Scan current role
2. Open required ports or close the rest of ports (Often firewall --> Predefined rules)
3. Enable minimum services and disable the rest