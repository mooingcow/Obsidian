
# 04 Forensic Tools
---

## Digital Forensic Tools
---
### Evaluating Tool Needs
- consider open source tools
    - best value for many features
- questions to ask
    - which os it run on
    - what file systems to analyse
    - can scripting lang be used with tool to automate repititive funcs?
    - have automated features?
    - vendor's reputation for support?
---

## Types of Tools
---
#### Hardware Forensic Tools
- range from single purpose components to complete comp systems and servers
- [[Chapter 4 - Forensic Tools#Hardware Tools|more info]] 

#### Software Forensic Tools
- up to $300
- types
	- command line apps
	- [[Chapter 4 - Forensic Tools#GUI Tools|gui apps]] 
- commonly used to copy data from suspect's disk drive to image file
---

## 5 Functions of Forensics Tools
---
#### Tasks Performed by Digital Forensic Tools
- follow guidelines by NIST's computer forensic tool testing (CFTT) program
    - ISO standard 27037 states that digital evidence first responders (DEFRs) should use validated tools
- all comp forensic tools (hardware and software) perform specific funcs (split into 5 categories)
	- acquisition
	- validation and verification
	- extraction
	- reconstruction
	- reporting
---
### Acquisition
---
- **making copy of orig drive**
- subfunctions:
    - physical data copy
    - logical data copy
        - logical partition
    - data acquisition format
        - raw data format
    - gui acquisition
    - remote, live (logon) and memory acquisition
- 2 data copying methods:
    - physical copying of entire drive
    - logical copying of disk partition
- formats for disk acquisition vary
    - from raw data to vendor-specific proprietary
- can view contents of raw img with hex editor

![](https://i.imgur.com/Pe2YToQ.png)
- creating smaller segmented files is typical feature in vendor acq. tools
    - segmented files are smaller and hence can be stored in smaller media
- remote acquisition of files is common in larger organisations
    - popular tools like accessdata and encase can do remote acquisition of forensics drive images on network
---
### Validation and Verification
---
- validation
    - way to confirm that tool is functioning as intended
        - ensure integrity of data copied
- verification
    - prove that 2 sets of data are identical by calculating hash or using similar method
    - related process: **filtering**
        - involves sorting and searching through investigation findings to seperate good and suspicious data
- subfunctions
    - hashing
        - ensure data not changed
        - CRC-32, MD5, SHA-1
    - filtering
        - separate good files and files that need to be investigated
        - based on hash value sets
    - analysing file headers
        - check on change file type
        - discriminate files based on types
- national software reference lib (NSRL) has compiled list of known file hashes
    - for variety of OS, apps and imgs
- validation and discrimination ^c154ef
    - many computer forensics programs include list of common header values
        - can see whether file extension is incorrect for file type
    - most tools can identify header values
---
### Extraction
---
- recovery task in digital investigation
    - most challenging to master
- recovering data is 1st step in analysing investigation's data
- subfunctions
    - data viewing
        - different tools provide different way of viewing data
        - keyword searching
            - good function but if wrong keyword used may produce "noise"
            - speeds up analysis for investigators
        - decompressing
        - carving ^5b53b6
            - reconstructing fragments of files
        - decrypting
            - potential problem for investigators
            - password recovery tools have feature for generating password lists
                - AKA password dict attack
                - if fails, can run brute force attack
        - bookmarking/tagging
---
### Reconstruction
---
- **purpose:**
	- recreate suspect drive to show what happened during crime or incident
    - create copy of suspect drive for other investigators
- methods
    - disk to disk copy
    - partition to partition copy
    - image to disk copy
    - image to partition copy
    - rebuilding files from data runs and [[Chapter 4 - Forensic Tools#^5b53b6|carving]] 
- to recreate image of suspect drive
    - copy image to another location/partition/physical disk or virtual machine
    - simplest method use tool to make direct disk to image copy
        - linux dd command
        - prodiscover
        - voom technologies shadow drive
---
### Reporting
---
- to perform forensic disk analysis and examination, need to create report
- subfunctions
    - bookmarking/tagging
    - log reports
        - document investigation steps
    - report generator
- use this information when producing final report
---

## Considerations for Tools
---
- **considerations:**
    - flexibility
    - reliability
    - future expandability
- create software lib with older vers of forensic utilities, OS and other programs
---

## GUI Tools
---
- can simplify investigation 
    - also simplifies training for beginner examiners
- generally a suite of tools
- **advantages:**
    - ease of use
    - multitasking
    - dont need learn older OS
- **disadvantages:**
    - excessive resource requirements
        - eg. RAM
    - inconsistent results because of type of OS used
        - eg. 32 bit vs 64 bit
    - create tool dependencies
        - investigators may want to use only 1 tool
            - refuse to change
        - should be familiar with more than 1 type of tool
---

## Hardware Tools
---
- **hardware considerations:**
	- technology changes rapidly
	- hardware eventually fails
	- schedule equipment replacements periodically
- **budget considerations:**
    - amount of time expected for workstation to be running
    - how often it fails
    - consultant and vendor fees
    - anticipate equipment replacement
        - more you use, more likely equipment will break
---

## Forensic Workstations
---
- **categories:**
    - stationary
    - portable
    - lightweight
- balance what you need and what your system can handle
    - RAM and storage need updating as tech advances
-  keep a hardware & software library
- police agency labs
    - need many options
    - use several pc configs due to diverse investigations
- private corporate labs
    - handle only system types used in organisation
- not difficult to build
    - **advantages**
        - customised to needs
        - save money
    - **disadvantages**
        - hard to find support for problems
        - can become expensive if careless
- need to identify what you intend to analyse
---
### Recommendations for Forensic Workstations
- workstations designed for forensics
- available vendor support saves time and frustration
- mix and match components to get capabilities needed
- determine where data acquisition will take place
    - eg. acquire data in field, may want to carry something light
- for stationary and lightweight workstations,
    - full tower to allow expansion devices
    - as much memory and processor power as budget allows
    - different sizes of hard drives
    - 400w or better power supply with battery backup
    - external firewire and usb 2.0 ports
    - assortment of drive bridges
    - ergonomic keyboard and mouse
    - good gpu + >17 inch monitor
    - high end gpu and dual monitors
- if limited budget, 1 option for outfitting lab is to use high end game pc
    - can perform well with modifications
---

## National Institute of Standards and Technology Tools
---
- NIST publishes articles, provides tools and creates procedures for testing/validating forensics software
- computer forensic tool testing (CFTT) project
    - manages research on comp forensics tools
- NIST created criteria for testing comp forensic tools based on
    - standard testing methods
    - ISO 17025 criteria for testing items that have no current standards
- lab must meet these criteria
    - establish categories for tools
    - identify forensic category requirements
    - develop test assertions
        - based on requirements, create tests to test tool's capability
    - identify test cases
    - establish test method
    - report test results
- ISO 5725 - specifies result must be repeatable and reproducible
- NIST created national software ref lib (NSRL) project
    - collects all known hash for commercial software apps and OS files
        - uses SHA-1 to generate known set of digital sigs called **Reference Data Set (RDS)**
    - helps filter known info
        - can help speed up invesigation time
    - can use **RDS** to locate and identify known bad files
---

## Validating and Testing Software
---
- important for evidence you recover and analyse to be admitted in court
- test and validate software to prevent damaging evidence

### Validation Protocols
- always verify results by doing same tasks with other tools
    - use at least 2
        - retrieving and examination
        - verification
- understand how forensics tools work
- 1 way to compare results and verify new tool is using disk editor like hex workshop or winhex
    - disk editor can view data on disk in raw format
    - dont have flashy interface
        - still reliable
        - can access raw data
- **computer forensic examination protocol**
    1. perform investigation with gui tool
    2. verify results with disk editor
    3. compare hash with both tools
- **digital forensics tool upgrade protocol**
    - ensure evi data wont be corrupted, we need to test:
		- new releases for tools
		- os patches and upgrades
	- if find problem, report to forensic tool vendor
		- dont use tool until problem fixed
	- use test hard disk for validation tests
	- check web for new editions, updates, patches and validation tests for tools
---

## Write-Blocker
---
- prevents data writes to hard disk
    - any tool that permits read only access to data storage devices w/o compromising integrity of data

#### software enabled blockers
- configure OS to monitor and filter drive I/O commands sent from OS
- typically run in shell mode (windows cli)
	- eg. pdblock from digital intelligence

#### hardware blockers
- write blocking software installed on a controller chip inside a portable physical device
- ideal for gui forensic tools
	- prevent windows/linux from writing data to blocked drive
- act as bridge between suspect drive and forensic workstation
---
### Using Write-Blockers
- can navigate to blocked drive with any app
    - no problem accessing blocked drive's apps after write-blocker is installed
- discards written data from os if data copy successful
- connecting tech
    - firewire
    - usb 2.0 and 3.0
    - sata, pata and scsi controllers
---

## Summary
---
![](https://i.imgur.com/2EMYQHl.png)
![](https://i.imgur.com/0UyP4um.png)
