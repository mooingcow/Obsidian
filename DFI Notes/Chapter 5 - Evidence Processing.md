	
# 05 Evidence Processing
---

## File Systems
---
- file system - gives os road map to data on disk
    - type of file system used determines how data is stored on disk
---

## Boot Sequence
---
- **complementary metal oxide semiconductor (CMOS)**
    - computer stores system config and date and time info here
    - cmos should be modified to boot from forensic floppy disk or cd
        - prevent evidence from hard disk being overwritten
- **basic input/output system (BIOS)** or **extensible firmware interface (EFI)**
    - contains programs that perform input and output at hardware level
- **bootstrap process**
    - contained in rom, tells comp how to proceed
    - displays key or keys u press to open the cmos setup screen
        - besides date and time, bios settings also stored in cmos
- BIOS can configure:
    - system time date
    - boot sequence
    - plug and play
    - mouse or keyboard
    - drive config
    - security
    - power management
    - etc.
---

## Disk Drives
---
- made up one or more platters coated with magnetic material
- components
    - geometry (how data is stored)
    - head
    - tracks
    - cylinders
    - [[Chapter 5 - Evidence Processing#Sectors|sectors]] (typically 512 bytes) ^a3dd02

![](https://i.imgur.com/13ECExz.png)
![](https://i.imgur.com/W0Ci88R.png)

- properties handled at drive's hardware/firmware level include
    - zone bit recording (ZBR)
        - grouping tracks by zones ensures all tracks hold same amount of data
    - track density
        - space between each track
        - smaller space = more track on platter
    - areal density
        - num of bits in 1 sq inch of disk platter
    - head and cylinder skew
        - improve disk perf by minimising movement of read/write head
---

## Solid State Storage Devices
---
- all flash memory have feature called **wear-leveling**
    - internal firmware feature used in SSD that ensures even wear of read/write for all memory calls
        - in general memory cells can perform 10k to 100k read/writes
- when dealing with SSD, make full forensic copy asap
    - in case need recover data from unallocated disk space
    - wear levelling feature auto overwrites the unallocated space
---

## Microsoft File Structures
---
#### Clusters
- **[[Chapter 5 - Evidence Processing#^a3dd02|sectors]]** grouped together to form clusters
- can have one or more sectors
- combining sectors minmises overhead of writing/reading files to disk
- clusters numbered sequentially starting at 0 in NTFS and 2 in FAT
    - 1st sector of all disks contains system area, boot record and file structure db
- OS assigns these cluster numbers called **logical addresses**
    - address point to relative position
---
#### Sectors
- sector numbers called **physical addresses**
    - from address 0 to last sector on disk
- clusters and their addresses are specific to logical disk drive which is **[[#Disk Partitions|disk partition]]**
---
#### Disk Partitions
- partition is a logical drive (e.g C:, D:, E:)
    - windows OS can have 3 primary partitions and extended partition that can contain 1 or more logical drives

##### Partition Gap
- unused space between partitions
- can be used to hide data

![](https://i.imgur.com/mmJXMqa.png)

##### Partition Table
- a table maintained on disk by OS describing partitions on disk
- key hex codes used by OS to identify and maintain file system
- is in [[Chapter 5 - Evidence Processing#Master Boot Record MBR|Master Boot Record]] sector 0

![](https://i.imgur.com/qlbNz5f.png)

##### Master Boot Record (MBR)
- located at sector 0 of disk drive
- precedes 1st partition
- MBR stores info abt partitions on disk and their locations, size and other important items
- in hex editor, can find 1st partition at offset 0x1BE
    - file system's hex code is offset 3 bytes from 0x1BE for 1st partition
    - sector address of where this partition start on drive is offset 8 bytes from 0x1BE
    - number of sectors assigned to partition are offset 12 bytes from 0x1BE

![](https://i.imgur.com/guw7zEz.png)

---

## FAT Disks
---
- file allocation table (FAT)
    - file structure db that microsoft originally designed for floppy disks
- FAT db typically written to disk's outermost track and contains
    - filenames
    - directory names
    - date and time stamps
    - starting cluster number
    - file attributes
- 4 current fat vers
    - FAT12
    - FAT16
    - FAT32
    - exFAT
        - used by xbox systems
---
#### Cluster Sizes 
- vary according to disk drive size and file system

![](https://i.imgur.com/CVvP5ul.png)

- microsoft os allocate disk space for files by clusters
    - results in **drive slack**
        - unused space in cluster between end of active file and end of cluster
- drive slack includes:
    - **ram slack**
        - portion of last sector used in last assigned cluster
    - **file slack**
        - unused space allocated for file
- unintentional side effect of FAT16 having large clusters was that it reduced fragmentation
    - as cluster size increased
---
#### Example
![](https://i.imgur.com/mO2OYCN.png)
- document size is 5000 bytes of data
	    - assuming hard disk size is 1.6gb and os allocates about 32,000 bytes or 64 sectors
    - unused space of 27,000 bytes is **file slack**
    - **ram slack** is portion of last sector (10th sector) used in last assigned cluster
        - remaining sectors are **file slack**
- **NOTE:**
    - data used to fill 120byte void (ram slack) is pulled from ram
	- any info in RAM from then on like login ID or password is placed in ram slack
---
#### Chaining Clusters
- when alloccated cluster runs out of space,
    - os allocates another cluster which creates more slack space on disk
- as files grow and need more space, assigned clusters chained together
    - chain can be broken or fragmented due to deleted files or expansion files
- when os stores data in FAT file system, it assigns starting cluster position to a file
    - data for file written to first sector of first assigned cluster
    - when first cluster filled and runout of space, FAT assigns next available cluster to file
---
#### Deleting FAT Files
- in microsoft os, when file deleted,
    - directory entry is marked as deleted file
        - with hex E5 char replacing 1st letter of filename
        - FAT chain for that file set to 0
- **data in file remains on disk drive**
- area of disk where deleted file resides becomes **unallocated disk space**
    - available to receive new data from newly created files or other files needing more space
---

## NTFS Disks
---
- nt file system (NTFS)
    - introduces in windows nt
    - primary file system for window 8 or later
- improvements over FAT
    - provides more information about a file
    - gives more control over files and folders
- is a journaling file system
    - records transaction before system carries it out (e.g. deleting a file)
    - in NFTS, everything written to disk considered a file
- on NTFS disk,
    - 1st data set is **partition boot sector**
    - next is **master file table (MFT)**
- ntfs results in less file slack space
    - clusters smaller for smaller disk drives
- also uses unicode
    - international data format

![](https://i.imgur.com/4aBTkNh.png)

---
#### NTFS System Files
- master file table (MFT) contains info abt all files on disk
    - including system and file os uses
- in mft, 1st 15 records reserved for system files
- records in mft are called **metadata**
![](https://i.imgur.com/A6RsmZJ.png)

---
#### MFT and File Attributes
- in ntfs mft
    - all files and folders stored in separate records of 1024 bytes each
- each record contains file or folder info
    - info divided into **record field** containing metadata
    - record field referred as **attribute id**
- file or folder information stored as **resident** or **non-resident** in the mft record
	- each mft record starts with header identifying it

##### Resident vs Non-Resident
###### Resident
- 512 bytes or less
- metadata and data stored in mft record

![](https://i.imgur.com/dXyx7Bn.png)

###### Non-Resident
- larger than 512 bytes
- stored outside mft
- mft record provides cluster addresses where file is stored on drive's partition
	- AKA **data runs**

![](https://i.imgur.com/EHClmqD.png)

![](https://i.imgur.com/LiTlkIf.png)
![](https://i.imgur.com/WZrLo2u.png)

##### NTFS Clusters
- when disk created as ntfs file structure, OS assigns logical clusters to entire disk partition
    - called **logical cluster numbers (LCNs)**
    - becomes address that allow mft to link non-resident files on disk's partition
- when 1st data written to nonresident files, LCN address assigned to file
    - LCN becomes file's **virtual cluster number (VCN)**

![](https://i.imgur.com/V24sLKJ.png)

##### MFT Structures for File Data
- for header of all mft records, record fields of interest are
    - offset 0x00
        - mft record identifer file
    - offset 0x14
        - length of header
        - indicates where next attribute starts
        - eg. `38 00` > `00 38` = 56 bytes
            - idk what this is
    - offset 0x1C to 0x1F
        - size of mft record
    - offset 0x32 and 0x33
        - update sequence array - stores last 2 bytes of 1st sector of mft record
            - used as checksum for record integrity validation

![](https://i.imgur.com/vmwTC7f.png)

- standard info attribute
    - create date and time
    - last modified date and time
    - last access "
    - record update "
![](https://i.imgur.com/JjFhgHe.png)

---
#### NTFS Alternate Data Streams
- alternate data streams
    - ways data can be appended to existing files
    - can obscure valuable evidentiary data intentionally or by coincidence
- in ntfs, alternate data stream becomes extra file attribute
    - allows file to be associated with diff apps
- can tell whether file has data stream attached by examining file's MFT entry

![](https://i.imgur.com/tArNx35.png)

---
#### NFTS Compressed Files
- ntfs provides compression similar to FAT
    - under ntfs, files, folders or entire volumes can be compressed
- most computer forensic tools can uncompress and analyse compressed windows data
---
#### NTFS Encrypting File System (EFS)
- EFS
    - introduced in windows 2000
    - implements pub key and priv key method of encrypting files, folders or disk volumes
- when EFS used in win2000 or later
    - **recovery cert** generated and sent to local windows admin account
        - recovery cert is required if there's problem
- users can apply EFS to files stored on local workstations or remote server

###### EFS Recovery Key Agent
- recovery key agent implements recovery cert
    - which is in windows admin acc
- windows admins can recover key in 2 ways
    - through windows
    - from MS-DOS command prompt
- MS-DOS commands
    - cipher (for ntfs only)
    - copy
    - efsrecvr
        - used to decrypt efs files
        - for ntfs only
    - use <command> \<command\> /? to find out more
---
### Deleting NTFS Files
- when file deleted in windows nt and later
    - os renames it and moves to recycle bin
- can use del MS-DOS command to del file
    - this method doesnt rename and move deleted file to recycle bin but eliminates file from mft listing in same way FAT does
---

## Whole Disk Encryption (WDE)
---
- **personal identity info (PII)** and trade secrets theft raised concerns
    - especially theft of laptop and computers
    - to prevent loss of info, software vendors provide **whole disk encryption (WBE)**
- whole disk encryption tools encrypt each sector of drive separately
- many of these tools encrypt drive's boot sector
	- to prevent any efforts to bypass secured drive's partition
- to examine encrypted drive need to decrypt it first
    - run vendor-specific program to decrypt drive
    - many vendors use bootable cd or usb drive that prompts for one-time passphrase
    - without credentials to unlock encrypted drive, impossible to view any logical level info

###### Features
- preboot auth
    - single sign-on password
    - fingerprint scan
- full or partial disk encryption with secure hibernation
    - password protected screen saver
- advanced encryption algos
    - AES or IDEA
- key management function
    - passphrase to reset pwd

#### Microsoft BitLocker (Example)
- hardware and software requirements
    - computer capable of running windows vista or later
    - **trusted platform module (TPM)** microchip ver 1.2 or newer
        - stores rsa encryption keys specific to host system for hardware authentication
    - computer BIOS compliant with trusted computing group (TCG)
    - 2 ntfs partitions
    - BIOS configured so hard drive boots first before checking other bootable peripherals
---

## Windows Registry
---
###### Registry
- db that stores:
	- hardware and software config info
	- network conns
	- user preferences 
	- setup info

###### View Registry
- regedit program for windows 9x later
- regedt32 for windows 2000, xp and vista
- both utilities can be used for win7 and later

###### Registry Terminology
- registry
- registry editor
- hkey
- key
- subkey
- branch
- value
- default value
- hives

![](https://i.imgur.com/VUJUmwH.png)
![](https://i.imgur.com/UZ76kQl.png)

---

## Microsoft Startup Tasks
---
- learn what files are accessed when windows starts
- this information helps you determine when suspect's computer last accessed
    - important with computers that might have been used after incident reported
---
### Startup in Win7 and Win8
- win 7/8 is multiplatform os
    - can run on desktops, laptops, tablets and smartphones
- boot process uses **boot config data (BCD) store**
    - bcd contains boot loader that initiates system's bootstrap process
        - press f8 or f12 when system starts to access advanced boot options
        - eg. in safe mode
---
### Startup in Windows NT and Later
- all ntfs computers perform these steps when it is turned on
    - power on self test (POST)
    - initial startup
    - boot loader
    - hardware detection and config
    - kernel loading
    - user logon

###### Startup Files for Windows Vista
- ntldr (NT loader) program in windows xp used to load OS replaced with these 3 boot utilities
	- bootmgr.exe
	- winload.exe
	- winresume.exe
- vista includes bcd editor for modifying boot options and updating bcd registry file
- bcd store (namespace container for bcd objects) replaces windows xp boot.ini file
	- old windows uses boot.ini to config boot sequences

###### Startup Files for Windows XP
- nt loader (NTLDR)
- boot.ini
- ntoskrnl.exe
- bootvid.dll
- hal.dll
- bootsect.dos
- ntdetect.com
- ntbootdd.sys
- pagefile.sys

![](https://i.imgur.com/JSyDUCG.png)

###### why need know startup process?
- contamination concerns in xp
	- when start xp ntfs pc, several files accessed immediately
		- last access data and timestamp for files change to current
		- destroys any potential evidence that shows when xp pc last used
---

## Virtual Machines
---
- vm
    - create representation of another computer of existing physical computer
    - is just few files on hard drive
        - must allocate space to it 
- vm recognises components of physical machine its loaded on
    - virtual os limited by physical machine's os as behaviour of virtual os can be affected by physical machine's os
        - certain operations may be blocked
- vm allows you to restore suspect's drive on vm
    - tests can be done and run nonstandard software that suspect might have loaded
- from network forensic standpoint, need to know some issues
    - vm used to attack another system on network
    - file slack, unallocated space etc. dont exist on vm so many standard items dont work on vms

###### Creating VM
- popular apps
    - vmware server
    - vmware player
    - vmware workstation
    - oracle vm virtualbox
    - microosft virtual pc
    - hyper-v
- using virtualbox
    - http://www.virtualbox.org/wiki/Downloads
---

## Summary
---
![](https://i.imgur.com/tR1ZqOG.png)
![](https://i.imgur.com/XhjZPrp.png)
![](https://i.imgur.com/IMCbyOE.png)
