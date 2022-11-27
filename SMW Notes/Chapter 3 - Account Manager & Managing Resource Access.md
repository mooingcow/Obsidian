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

## File Ownership
---
- Folders are first owned by the account that created them
- Folder owners have the ability to change permissions for the folders they create
- Ownership can be transferred by having:
	- Take Ownership advanced permission
	- Full Control permission (which includes Take Ownership)
---

## Configuring Shared Folders and Shared Folder Permissions
--- 
- A shared folder is a folder set up for users to access over the network
- Before sharing a folder --> Must first enable network sharing

###### Enabling Sharing
- Make sure File and Printer sharing is turned on 
- Network discovery turned on --> To view other network computers and devices

###### Configuring Sharing through Folder Properties 
- Set by configuring sharing using the FIle Sharing windows and the folder's Sharing tab in the Properties dialog box

Permissions:
- Read 
	- Users can view file and subfolder names, read data in files, and run programs
	- By default, the “Everyone” group is assigned “Read” permissions
- Change (Read/Write, Contribute) 
	- Users can do everything allowed by the “Read” permission 
	- Also can add files and subfolders, change data in files, and delete subfolders and files 
	- This permission is not assigned by default
- Full Control
	- Users can do everything allowed by the “Read” and “Change” permissions
	- Can change permissions for NTFS files and folders only
	- By default, the “Administrators” group is granted “Full Control” permissions
- Owner
	- Automatic assigned to the share owner, with same effective permission as Full Control 

###### Caching Folders
- Contents of the cached folder are available offline
	- Offline files can be synchronised with the network versions of the files
- Folders can be cached in 3 ways
	1. Only the files and programs specified will be available offline
	2. No files and programs form the shared folder are available offline
	3. All files and programs that user open from the shared folder are automatically available offline
- Access-based enumeration
	- Permits the user to only view folders and files which they have permissions

###### Configuring Sharing using Server Manager
- Offers an interface for managing permissions and shares from one tool

Server Message Block (SMB) protocol
- Enables an OS to offer shared files, folders, printers, serial ports, and other port communications on a network

Network File System (NFS) protocol
- Used for file and folder sharing on UNIX and Linux systems
- When installed on a Windows system share, it enables it to be accessed by UNIX and Linux computers 

File Server Resource Manager role service
-  Allows you to set folder quotas

###### Publish Shared Folder in Active Directory
- Make it available for users to access when they view Active Directory contents
- Makes it easier to find when a user searches for it

- Active Directory search capabilities are automatically built into all modern Winows OSs
- Objects can be published domain-wide or through an OU
---

## Troubleshooting a Security Conflict
---
- Using Effective Access allows you to view Effective Permissions assigned to a user or group
- Calculating Effective Permissions takes into account group membership as well as permission inheritance
- Accounts for copying or movement of folders or files:
	- A newly created file inherits the permissions already set up in a folder
	- A file that is copied from one folder to another on the same volume inherits the permissions of the folder to which it is copied
	- A file or folder that is moved from one folder to another on the same volume takes with it the permissions it had in the original folder
	- A file or folder that is moved or copied to a folder on a different volume inherits the permissions of the folder to which it is moved or copied
	- A file or folder that is moved or copied from an NTFS volume to a folder in a FAT or FAT32 volume is not protected by NTFS permissions
		- But it does inherit share permissions if they are assigned to the FAT/FAT32 folder
	- A file or folder that is moved or copied from a FAT volume to a folder in an NTFS volume inherits the permissions already assigned in the NTFS folder
---

## Configuring NTFS and Shared Folder Permissions
---
- When accessing a shared folder over the network, both NTFS and Share permissions are considered
- When NTFS and Share permissions are combined, the more restrictive permissions apply

###### Example
- John has NTFS Modify Permission to the Reports folder
- He is given Reader Share permission to the Reports folder
- If he logs in locally to the system and accesses Reports folder,  he can modify it (only NTFS permission applies)
- If he accesses Reports folder over the network, he has only Read permission (the more restrictive of the NTFS and Share permission)
---

## Important New Features in Windows Server 2016 Active Directory
---
###### Restart Capability
- Stop Active Directory Domain Services without taking down the computer
- After work on Active Directory is done, simply restart Active Directory Domain Services

###### Read-Only Domain Controller
- Cannot use it to update information in Active Directory and it does not replicate to regular DCs
- An RODC can still function as a Key Distribution Center for the Kerberos authentication method
- The purpose of having an RODC is for better security at branch locations
	- Where physical security measures might not be as strong as at a central office
- An RODC can also be configured as a DNS server

###### Cloning Domain Controllers
- Especially targeted for easier deployment of multiple domain controllers in an environment with multiple virtual machines
- Cloning cuts down on the steps required to create additional virtual domain controllers
- Server administrator can configure Active Directory --> Create a copy of the virtual domain controller
- Additional steps can be handled by running PowerShell cmdlets and using a PowerShell script to define configuration parameters

###### Fine-Grained Password Policy Enhancement
- Different security groups can have different password policies
- Windows Server 2012 R2 introduced the ability to use the Active Directory Administrative Center for managing password setting objects in the Active Directory schema
	- Makes server access more secure
	- Helps reduce errors made by server administrators when working with fine-grained passwords

###### Protected Users Global Group
- Enforces strict locked-in security and protection measures that cannot be reconfigured 
- Only way to change the security for a member of this group is to remove the member from the group
- User accounts, computers, printers, and servers can be members
- Security restrictions that apply to the protected users global group:
	- Group members cannot use weaker forms of authentication
	- The Kerberos Ticket Granting Ticket’s lifetime is limited to 4 hours, which means group member must be authenticated every 4 hours
	- Connections to system that do not utilize this global group may not succeed
	- Only higher-level encryption methods compatible with Kerberos security can be used
---

## Implementing User Profiles
--- 
- A local user profile is automatically created at the local computer when you log on with an account for the first time
	- The profile can be modified to consist of desktop settings that are customised for one or more clients who log on locally
- Advantages:
	- Multiple users can use the same computer and maintain their own customised setting
	- Profiles can be stored on a network server so they are available to users regardless of the computer they use to log on (roaming profile)
	- Profiles can be made mandatory so users have the same settings each time they log on (mandatory profile)
- One way to set up a profile is to first set up a generic account on the server with the desired desktop configuration
	- Then copy the Ntuser.dat file to the \\Users\\Default folder in Windows Server 2016
- To create the roaming profile, set up a generic account and customize the desktop
	- Set up those users to access a profile by opening the Profile tab in each user’s account properties and entering the path to that profile
--- 
