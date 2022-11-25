___

## User Account Management
---
- Default Accounts
	- Administrator & Guest
- Accounts can be set up in 2 environments:
	- Stand-alone server without Active Directory
	- A domain with Active Directory installed 
		- These accounts can be used to access any server or resource in the domain

###### Creating Accounts without Active Directory
- mmc in open box
- Select Local Users and Groups mmc snap-in

###### Creating Accounts with Active Directory
- Active Directory Users and Computers (Tools in Server Manager)

###### Disabling, Enabling, and Renaming Accounts 
- May disable accounts when someone leaves and re-enable for their replacement 

###### Moving an Account
-  When an employee moves form one department to another
- May need to move account from one container to another

###### Resetting a Password
- Administrator does not have the option to look up a password
	- Can reset passwords

###### Deleting an Account
- Good practice to delete that are no longer in use
- Its globally unique identifier (GUID) is also deleted and will not be reused even if you create another account using the same name

###### Recovery of Deleted Account
- Using Active Directory Recycle Bin
	- By default is off
- Forest functional level must be raised to Windows Server 2008 R2
- Enabling Active Directory Recycle Bin is irreversible
---

## Security Group Management
--- 
- Grouping accounts with similar characteristics
- Scope of influence (aka scope)
	- The reach of a group for gaining access to resources in Active Directory

###### Types of Groups
- Local (aka Machine Local)
- [[Chapter 3 - Account Manager & Managing Resource Access#Domain Local Groups|Domain Local]]
- [[Chapter 3 - Account Manager & Managing Resource Access#Global Groups|Global]]
- [[Chapter 3 - Account Manager & Managing Resource Access#Universal Groups|Universal]]

These groups can be used for security or distribution groups

###### Security Groups
-  Used to enable access to resources on a stand-alone server or in Active Directory
- Implemented via group membership

###### Distribution Groups
- Used for email or telephone lists, to provide quick, mass distribution of information
---

## Properties of Groups
--- 
- Properties of groups can be configured using:
	- Local Users and Groups (Local Groups)
	- Active Directory Users and Computers (Domain Groups)
- Properties are configured using:
	- General
	- Members
	- Member of
	- Managed by
---

## OU vs Security Membership
--- 
###### OUs
- Groups Policies are applied to OUs (e.g. Password Policies)
- Delegation of authority are also applied to OUs

###### Security Groups
- Used to assign resource permissions
	- File and folder permissions
	- Shared folder permissions
---

## AGDLP
---
###### Local Security Group
- Used to manage resources on a stand-alone computer that is not part of a domain and on member servers in a domain
- Accounts can be divided into local groups 
	- Each group given different security access based on the resources at the server

###### Domain Local Groups
- Used when Active Directory is deployed
- Scope of a domain local group is the domain in which the group exists
- Used to manage resources in a domain --> giving global groups access to the resources
	- DL groups provide access to resources --> servers, folders, shared folders, and printers etc.
- Should only be put in access control lists
	- Members of domain local groups should mainly be global groups

###### Global Groups
- Intended to contain user accounts from a single domain
- Can be set up as a member of a domain local group in the same or another domain
- Can contain user accounts and other global groups from the domain in which it was created
- Can be converted into a universal group 
	- As long as it is not nested in another global group or in a universal group
- Usually built with accounts that need access to resources in the same or different domain
	- Then make the global group a member of a domain local group in the same or different domain 

###### Universal Groups
- Provide an easy means to access resources spanning domains and trees
- Universal group membership can include:
	- User accounts from any domain
	- Global groups from any domain
	- Other universal groups from any domain

###### Guidelines for Groups
- Use global groups to hold accounts as members
- Use domain local groups to provide access to resources in a specific domain
- Use universal groups to provide extensive access to resources 

###### Implementation
Best Practices --> AGDLP/AGUDLP
- A - Account
- G - Global
- U - Universal
- DL - Domain Local
- P - Permissions
Variations:
- AP
- AGP
- AUP
- AGUP
The shorter the A to P distance:
- Easier to create
- More difficult to maintain (error prone)
---

## File Attributes
--- 
- Attributes are stored as header infromation with each folder and file 
	- Along with volume label, designation as a subfolder, and date & time of creation
- Two basic attributes remain in NTFS that are still compatible with FAT
	- Read-only and hidden
- NTFS offers advanced or extended attributes --> Accessed by clicking the General tab's Advanced button
	- Archive
	- Index 
	- Compress
	- Encrypt

###### Archive Attribute
- Indicates that the folder or file needs to be backed up because it is new or changed
- File server backup systems can be set to detect files with the archive attribute to ensure those files are backed up

###### Index Attribute
- NTFS index attribute is used to index the folder and file contents so that file properties can be quickly searche in Windows Server 2016 through the Indexing Service
- Windows Server 2016 offers newer, faster search service called Windows Search Service
	- Must first install File and Storage Services role via Server Manager

###### Compress Attribute
- Folder and contents can be stored on the disk in compressed format
- Advantage: 
	- Compression saves space while allowing you to work on them in the same way as umcompressed files
- Disadvantage:
	- Compressed files increase CPU overhead to open the files and copy them 
- Best Practices:
	- Busy servers that experience high-volume write or execute operations are poor candidates for compression 
	- Servers that are rarely busy or primarily have read traffic are acceptable candidates
	- Files that are rarely accessed or that are archived on the server can be candidates
	- User home folders on a server typically have high levels of read and write activity and should not be compressed

###### Encrypt Attribute
- Protect folders and files so that only the user who encrypts the folder or file is able to read it
- An encrypted folder or file uses the Microsoft Encrypting File System (EFS)
	- Sets up a unqiue, private encryption key associated with the user account that encrypted the folder or file
	- Using symmetric and asymmetric encryption technique
	- Folder remains encrypted even if it is renamed
- Best Practices:
	- Move files for encryption into specifically designated folders flagged for encryption
	- Safer for applicatoins to work on a file in an encrypted folder rather than work on a file that is individually encrypted
	- Workstation users and server administrators should consider encrypting My Documents and Documents folders on their systems
	- User and server administrators should frequently export certificates and private keys to portable media and store the media in a secure place
---

## File Permissions
--- 
- Control access to an object, such as a folder or file
- Example:
	- When a folder is configured so that the domain local group only has access to read the contents of a folder
		- You are configuring permissions
		- You are also configuring that folder's discretionary access control list (DACL) of security descriptors
- If need to customise permissions, can set up special permissions for a group or user
- Best Practices: 
	- Protect \\Windows folder that contains OS files on Windows from general users by allowing limited access
	- Protect server utility folders with access permissions only for Administrators, Server Operators, and Backup Operators groups 
	- Protect software application folders with read & execute & write to enable users to run applications and write temporary files
	- Create publicly used folders to have Modify access 
	- Provide users full control of their own home folders
	- Remove unnecessary access groups from confidential folders
	- Use Deny sparingly
---

## File Auditing
--- 
- Enables tracking of activity on a folder or file
- Windows Server 2016 NTFS folders and files enable auditing of the above activities (archiving, compression, encrypting) as advanced permissions
---

