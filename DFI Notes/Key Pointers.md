
# Key Pointers
---

## Chapter 1
---
### Digital Forensics
- application of computer science and investigative procedures for legal purposes involving the analysis of digital evidence

### Chain of Custody
^208f10
- Route evidence takes from time found until case is closed
- Maintain each record of the digital evidence from collection to presentation

### Case Law
###### what is case law
>law established by the **outcomes of former cases**

###### when is case law used
- allow legal counsel to apply prev similar cases to current case to **address ambiguity** in laws when **statutes do not exist**
- current laws cannot keep up with rate of tech change
- examiners must know recent court rulings on search & seizure in electronic environment

### Public vs Private Investigations
- [[Chapter 1 - Intro to Forensics#Digital Investigations|more info]] 

| Public | Private |
| ----------- | ----------- |
| Government Agencies | Private Companies and Lawyers | 
| Investigates criminal allegations follwing the legal process | Addresses company policy violations and litigation disputes |
| Searches for evidence showing that alleged crimes were committed | Searches for evidence to showing violation of company rules/attack on assets <br/><br/> Minimise risk to company|
| Requires Search Warrant | No warrant needed (must have good company policy to protect from litigation) |
___

## Chapter 2
---
### Rule of Computer Forensics
- always preserve original evidence
- evidence should be stored in **approved secure container** with limited access
- must make forensic copy of evidence before examining

### Chain of Evidence Form
- shows [[Key Pointers#Key Pointers#Chain of Custody|chain of custody]]
- helps document what has been done with original evidence and forensics copies
- [[Chapter 2 - Understanding Computer Investigations#Evidence Forms|Chapter 2 - Evidence Forms]] 

### Common Investigation Cases
- [[Chapter 2 - Understanding Computer Investigations#Private Sector High-Tech Investigations Examples|Chapter 2 - Common Investigation Cases]]
---

## Chapter 3
---
### Definition of Image
- file containing bit stream copy of all data on disk/partition
- [[Chapter 2 - Understanding Computer Investigations#Bit-Stream Copies|definition]] 

### Image File Formats
- [[Chapter 3 - Data Acquisition#Raw Format|raw format]]
- [[Chapter 3 - Data Acquisition#Proprietary Formats|proprietary format]] 
- [[Chapter 3 - Data Acquisition#Advanced Forensics Format AFF|advanced forensics format]] 

### Acquisition
- to create forensic copy of piece of media that is suitable to use as evidence in court of law
- [[Chapter 3 - Data Acquisition#Determining Best Acquisition Method|acquisition methods]] 

### Write Blocker
- [[Chapter 4 - Forensic Tools#Write-Blocker|write blockers]] 

### Validation Techniques
>validating evidence is most critical aspect of computer forensics
- CRC-32
- MD5
- SHA-1 - SHA-512
- [[Chapter 3 - Data Acquisition#Validating Data Acquisitions|more info]] 

### Remote Acquisition
- [[Chapter 3 - Data Acquisition#Remote Network Acquisition Tools|remote acquisition]] 
---

## Chapter 4
---
### Tool Needs
- which os it run on
- what file systems to analyse
- can scripting lang be used with tool to automate repititive funcs / have automated features?
- vendor's reputation for support?
- [[Chapter 4 - Forensic Tools#Types of Tools|hardware or software]] 
- function of tool (5 functions of tools)

### 5 Functions of Tools
###### acquisition
>making copy of original drive
- [[Chapter 4 - Forensic Tools#Acquisition|more info]] 

###### validation & verification
**validation**
> confirm that tool is functioning as intended and ensure integrity of data copied

**verification**
>prove that 2 sets of data are identical by calculating hash or using similar method

**filtering**
- separate good files and files that need to be investigated based on hash value sets
	- discrimate files based on types to see if file extension is incorrect
- [[Chapter 4 - Forensic Tools#Validation and Verification|more info]]

###### extraction
>recovering data in digital investigation
- [[Chapter 4 - Forensic Tools#Extraction|more info]] 

###### reconstruction
>recreate suspect drive to show what happened during crime or incident
- OR
>create copy of suspect drive for other investigators
- [[Chapter 4 - Forensic Tools#Reconstruction|more info]] 

###### reporting
>create report after forensic disk analysis and examination
- [[Chapter 4 - Forensic Tools#Reporting|more info]] 

### Validation Tests
- always verify results by doing same tasks with other tools
    - use at least 2
        - retrieving and examination
        - verification

###### computer forensic examination protocol
1. perform investigation with gui tool
2. verify results with disk editor
3. compare hash with both tools

###### **digital forensics tool upgrade protocol**
- ensure evi data wont be corrupted, we need to test:
	- new releases for tools
	- os patches and upgrades
- if find problem, report to forensic tool vendor
	- dont use tool until problem fixed
- use test hard disk for validation tests
- check web for new editions, updates, patches and validation tests for tools
- [[Chapter 4 - Forensic Tools#Validation Protocols|more info]] 
---

## Chapter 5
---
### Disk Partitions
-  before a drive (a,b,c,d) can be used by any OS, a [[Chapter 5 - Evidence Processing#Partition Table|partition table]] needs to be created on the drive
- [[Chapter 5 - Evidence Processing#Master Boot Record MBR|master boot record (MBR)]] is the information in the first sector of any hard disk that identifies how and where an operating system is located so that it can be boot (loaded) into the computer's main storage or random access memory 
	- MBR holds the information on how the logical partitions, containing file systems, are organised on that medium

### RAM Slack & File Slack
###### RAM slack
>portion of last sector used in last assigned cluster

###### file slack
>unused space allocated for file

###### calculations
- [[Chapter 5 - Evidence Processing#Clusters|cluster]] -> space required for a file is made up of number of [[Chapter 5 - Evidence Processing#Sectors|sectors]] 

**Number of Clusters Required to Store a File** 
```
(FileSize) / (ClusterSize) 
= Round Up (ClusterRequired)
```

- ClusterSize is determined by no. of sectors 

**RAM Slack** 
- Sector Size = 512 Bytes (in general)
```
(SectorsRequired) = (FileSize) / (SectorSize) = Round Up (SectorsRequired)

Round Up (SectorsRequired) * Sector Size = Total Sector Size Required

Total Sector Size – File Size = RAM Slack
```

**File Slack** 
```
File Slack = (SizeOfClusterRequired) – (FileSize) – (RAMSlack)
```

### FAT Disks
![[Chapter 5 - Evidence Processing#FAT Disks|more info]] 

### NTFS Disks
###### introduction
- nt file system (NTFS)
    - provides more information about a file
    - gives more control over files and folders
- is a journaling file system
    - records transaction before system carries it out (e.g. deleting a file)
    - in NFTS, everything written to **disk considered a file**
- on NTFS disk,
    - 1st data set is **partition boot sector**
    - next is **master file table (MFT)**
- uses unicode
    - international data format

###### master file table
- contains info abt all files on disk
    - including system and files os uses
- 1st 15 records reserved for system files
	- records in mft are called **metadata**
![](https://i.imgur.com/A6RsmZJ.png)
 - all files and folders stored in separate records of 1024 bytes each
- each record contains file or folder info
    - info divided into **record field** containing metadata
	- AKA **attribute id**
- file or folder information stored as **resident** or **non-resident** in the mft record
	- each mft record starts with header identifying it

###### file attributes
##### resident
- 512 bytes or less
- metadata and data stored in mft record
- [[Chapter 5 - Evidence Processing#Resident|more info]] 

##### non-resident
- larger than 512 bytes
- stored outside mft
- mft record provides cluster addresses where file is stored on drive's partition
	- AKA **data runs**
	- [[Chapter 5 - Evidence Processing#NTFS Clusters|ntfs clusters]]  
- [[Chapter 5 - Evidence Processing#Non-Resident|more info]] 

###### mft structures for file data
- [[Chapter 5 - Evidence Processing#MFT Structures for File Data|more info]] 

### Windows Registry
- [[Chapter 5 - Evidence Processing#Windows Registry|more info]] 
---

## Chapter 6
---
### Scope Creep
 - when inves. expands beyond original description due to unexpected evidence
- attorneys may ask investigators to examine other areas or more evidence
- increasing time and resources needed to extract, analyse and present evidence

### Hex Editors
- hashing specific files or sectors
	- with hash val, use tool to search for suspicious file that might have name changed to look innocent
- use hash vals to **[[Chapter 4 - Forensic Tools#^c154ef|discriminate data]]** 
    - AccessData has own hashing db AKA **known file filter (KFF)**
	    - KFF filters known program files from view and contain hash values of known illegal files
	    - compares file hash with files on evidence drive if contain suspicious data
    - WinHex provides md5 and sha-1 hashing algorithm
	    - also has bit-shifting feature

### Data Hiding Techniques
###### data hiding
>changing/manipulating file to conceal info

###### techniques
##### hiding files using OS 
- [[Chapter 6 - Analysis & Validation#Hiding Files using OS|info]]
##### hiding partitions
- [[Chapter 6 - Analysis & Validation#Hiding Partitions|info]] 
##### marking bad clusters
- [[Chapter 6 - Analysis & Validation#Marking Bad Clusters|info]]
##### bit-shifting
- [[Chapter 6 - Analysis & Validation#Bit-Shifting|info]] 
##### encrypted files
- [[Chapter 6 - Analysis & Validation#Examining Encrypted Files|info]] 
##### password protection
- [[Chapter 6 - Analysis & Validation#Recovering Passwords|info]] 

### Steganography & Watermarking
###### steganography
>hiding msg where only the intended recipient knows its there
- hide data using steganography tools 
	- [[Chapter 6 - Analysis & Validation#using steganography tools|more info]] 

###### steganalysis
>detecting and analysing steganography files
- [[Chapter 6 - Analysis & Validation#steganalysis methods|methods]] 

###### digital watermarking
>a marker secretly embedded in audio, video, or image data to protect and identify file ownership
- only found under certain conditions 
	- e.g. using some algorithm
	- usually not visible after using steganography
![[Chapter 6 - Analysis & Validation#^56429d]] 
---

## Chapter 7
---
### Certifications & Trainings
- [[Chapter 7 - Digital Forensics Lab#Certification and Training|info]]

### Physical Requirements for Lab
- small room with true floor-to-ceiling walls
- door access with locking mechanism
- secure container
- visitor's log
- ppl working together should have same access level
- brief staff about security policy
- must be secured so
	- should be secure so evidence not lost/corrupted/destroyed

### Evidence Containers
- [[Chapter 7 - Digital Forensics Lab#Using Evidence Containers|info]]

### Physical Security
- [[Chapter 7 - Digital Forensics Lab#Physical Security Needs|info]] 

### Auditing Forensics Lab
- [[Chapter 7 - Digital Forensics Lab#Auditing Forensics Lab|info]] 

### Forensic Workstation
- [[Chapter 7 - Digital Forensics Lab#Selecting Forensic Workstation|info]] 
---

## Chapter 8
---
### Digital Evidence
- any info stored/transmitted in digital form
- diff between document evidence and digital evidence
    - document evidence always visible on its face

### Tasks Performed with Digital Evidence
- identify digital info/artifacts that can be used as evi
- collect/preserve/document evi
- analyse/identify/organise evi
- rebuild evi or repeat situation to verify that results can be reproduced reliably
- ![](https://i.imgur.com/PumUMSF.png)

### Rules of Evidence
###### good practices
- handle evidence consistently to help verify work and enhance credibility

###### best evidence rule
- to prove content of written doc/recording/photo, the orignal is required
- allow duplicate when its produced by same impression as original
	- not always possible to produce orig
	- eg. when cannot use original evidence
		- network servers - cannot remove from network to acquire evidence since will cause harm to business/owner (innocent)
- data can be admitted in court as long as bit-stream copies of data created and maintained
    - though not best evidence

###### other rules
- computer record generally considered **hearsay** evidence
	- **hearsay:** second hand/indirect evidence
- computer records admissible if its a business record

###### computer records
- [[Chapter 8 - Crime & Incidence Scene Processing#Computer Records|info]] 

###### properties of evidence
- admissible
- authentic
- complete
- reliable
- believable

### Collecting Evidence in Private-Sector
- corporate policy 
	- stating right to inspect computing assets at will
		- i.e displaying a warning banner or publish company’s policy
- [[Chapter 8 - Crime & Incidence Scene Processing#Collecting Evidence in Private-Sector Incident Scenes|more info]] 

### Preparing for a Search
- [[Chapter 8 - Crime & Incidence Scene Processing#steps|steps]] 
- [[Chapter 8 - Crime & Incidence Scene Processing#determine tools needed|tools needed]] 

### Ways to Store Digital Evidence
- [[Chapter 8 - Crime & Incidence Scene Processing#Storing Digital Evidence|info]] 
---

## Chapter 9
---
### How do Cellphones Work?
###### mode of communication
- [[Chapter 9 - Celluar Mobile Networks#mode of communication|info]] 

###### celluar layout
- [[Chapter 9 - Celluar Mobile Networks#cellular layout|info]] 

###### celluar division
- [[Chapter 9 - Celluar Mobile Networks#cellular division|info]] 

### Data Transmission
###### MTSO
[[Chapter 9 - Celluar Mobile Networks#MTSO|info]] 

###### celluar hand-off
- [[Chapter 9 - Celluar Mobile Networks#cellular hand-off|celluar hand-off]] 
- [[Chapter 9 - Celluar Mobile Networks#hard vs soft hand-off|hard vs soft hand-off]] 

### Access Technologies
 - iDEN (integrated digital enhanced network)
	- 2G
	- digital
	- [[Chapter 9 - Celluar Mobile Networks#iDEN|more info]] 
- CDMA (code division multiple access)
	- 2G/3G
	- digital
	- [[Chapter 9 - Celluar Mobile Networks#CDMA|more info]] 
	- [[Chapter 9 - Celluar Mobile Networks#CDMA Family|CDMA Family]] 
	- [[Chapter 9 - Celluar Mobile Networks#BitPIM Software for CDMA|BitPIM Software for CDMA]] 
	- [[Chapter 9 - Celluar Mobile Networks#Qualcomm for CDMA|Qualcomm for CDMA]] 
- GSM (global system mobile communication)
	- 2G
	- digital
	- [[Chapter 9 - Celluar Mobile Networks#GSM|more info]] 

### Cell Phone Identification Numbers
###### MIN
![[Chapter 9 - Celluar Mobile Networks#Mobile Identity Number MIN]]

###### MEID
![[Chapter 9 - Celluar Mobile Networks#Mobile Equipment ID MEID]]

###### IMEI
![[Chapter 9 - Celluar Mobile Networks#International Mobile Equipment Identity IMEI]]
![[Chapter 9 - Celluar Mobile Networks#IMEI Checksum Verification|checksum verification]]
___

## Chapter 10
---
### Android OS
- a non-proprietary, open standard mobile operating system based on a modified version of the linux kernel
- developed by the Open Handset Alliance (OHA)
	- in charge of the Android smartphone operating system
	- created by Google and includes key members such as China Mobile, HTC, Intel, Motorola, NTT DoCoMo, Sprint, and T-Mobile USA
	- a group of more than 50 mobile technology companies working together

### Android Architecture
![[Chapter 10 - Android Forensics#Android Architecture]] 

### Acquisition
###### seizure & isolation
![[Chapter 10 - Android Forensics#Seizure and Isolation]] 

###### prerequisites
- [[Chapter 10 - Android Forensics#Prerequisites|info]] 

###### types of acquisitions
![[Chapter 10 - Android Forensics#Types of Acquisitions]] 

###### ways to store data
- [[Chapter 10 - Android Forensics#Ways to store data|info]] 
---

## Chapter 11
---
## Acquisition
###### seizure & isolation
![[Chapter 11 - iOS Forensics#Seizure and Isolation]] 

###### types of acquisition
![[Chapter 11 - iOS Forensics#Types of Acquisition]]

### iOS Architecture
![[Chapter 11 - iOS Forensics#iOS Architecture]]

### File System
###### file system
- [[Chapter 11 - iOS Forensics#iOS File System|info]] 

###### partitions
- [[Chapter 11 - iOS Forensics#Partitions|info]] 

###### file types
![[Chapter 11 - iOS Forensics#File Types]] 

###### data structure & artifacts
- [[Chapter 11 - iOS Forensics#Data Structure and Artifacts|info]] 

### iOS Devices
- [[Chapter 11 - iOS Forensics#iOS Devices|info]] 
---

## Chapter 12
---
### Rooting in Android
- to unlock the operating system so you can 
	- install unapproved apps
	- deleted unwanted bloatware
	- update the OS
	- replace the firmware
	- customize anything 
- allow user to gain “root” user privileges
	- no restriction on system settings after rooted

### Jailbreaking in iOS
- requires modification of OS settings
- a form of privilege escalation via hardware / software exploits
- enable installation of 3rd party apps

### Impacts of Jailbreaking
- voiding of warranty
- error and performance issues (not tested)
	- could cause phones become unstable
- may violate EULA (end-user license agreement) and organisation’s security policy on permitted activities with corporate devices

### Motivation for End Users
- more application sources
- access unauthorised applications
	- pirated software & Firefox in iPhone
- remove vendor-installed bloatware
	- improve performance
	- increase available memory (RAM/ROM)
- access restricted hardware resources
	- i.e. bluetooth on Kindle Fire (tablet from Amazon)
	- perform system tweaking

### Tools Used
![[Chapter 12 - Rooting and Jailbreaking#iOS]]
![[Chapter 12 - Rooting and Jailbreaking#android]]
___
