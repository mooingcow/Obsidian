
# 06 Analysis and Validation
---

## What Data to Collect and Analyse
---
- depends on nature of inves. AND amt to process
    - investigators often locate and recover specific items like emails - simplify speed processing
- **scope creep** - when inves. expands beyond original description
    - due to unexpected evidence
    - attorneys may ask investigators to examine other areas or more evidence
    - increasing time and resources needed to extract, analyse and present evidence
    - document extra time spent on recovering extra evidence
- scope creep more common now
    - criminal inves. needs more detailed examination of evidence just before trial
    - helps prosecutors fend off attacks from defence attrneys
- new evidence discovered often isnt revealed to prosecution
    - more impt for prosecution teams to ensure they analysed evidence exhaustively before trial
---

## Digital Forensics Cases
---
- begin case with inves. plan that defines
    - goal and scope of inves.
    - materials needed
    - tasks to do
- approach depends on type of case
    - **corporate**
        - easier due to easy access to evidence
    - **criminal**
        - more difficult due to scope
            - eg. need contact ISP to gather evidence
    - **civil**

###### Basic Steps
1. for target drives, use recently wiped media that is reformatted and inspected for viruses
2. inventory the hardware on suspect's computer
	- note condition of the computer too
3. for **[[Chapter 3 - Data Acquisition#^3d124f|static acquisitions]]**, remove original drive and check date and time values in system's CMOS
4. record how u acquire data from the drive
5. process drive content methodically and logically
    - eg. emails > jpg > spreadsheet > word
6. list all folders and files on drive
    - note where xx file found
7. recover file content for all password protected files
    - use password recovery tools
8. identify function of every exe file that dont match hash vals
    - if needed run file for more info
9. maintain control of all evidence and findings

###### Refining and Modifying the Investigation Plan
- sometimes need to deviate from initial plan and follow evidence
- know data types to look for
- key to start with plan but be flexible
---

## Analysing and Validating Data
---
### Using OSForensics to Analyse Data
- osforensics support these file systems
    - microsoft FAT12, FAT16, FAT32
    - microsoft NTFS
    - mac HFS+ and HFSX
    - linux EXT2fs and EXT4fs
- can analyse data from many sources
    - includes image files from other vendors

![](https://i.imgur.com/t87lZS7.png)

---
### Validating Forensic Data
- ensure integrity of data essential for presenting evidence in court
- tools offer hashing of image files
    - eg. prodiscover runs hash and compares hash with original hash when loaded file

###### Validating with Hex Editors
- some tools have limitations for hashing so use advanced hex editors for data integrity
- advanced hex editors have features not in forensic tools
    - hashing specific files or sectors
    - with hash val, use tool to search for suspicious file that might have name changed to look innocent
- winhex provides md5 and sha-1 hashing algorithm

![](https://i.imgur.com/YHve4VE.png)

- use hash vals to **[[Chapter 4 - Forensic Tools#^c154ef|discriminate data]]** 
    - AccessData has own hashing db AKA **known file filter (KFF)**
    - KFF filters known program files from view and contain hash values of known illegal files
    - compares file hash with files on evidence drive if contain suspicious data
    - other tools can import the **National Software Reference Library (NSRL) db** and run hash comparisons

###### Validating with Digital Forensics Tools
- prodiscover
    - .eve files have metadata with hash val
    - has preference u can enable for auto verify image checksum feature when files loaded
        - if auto verify image checksum and hash in .eve metadata dont match, prodiscover will notify that acquisition is corrupted and not reliable evidence

![](https://i.imgur.com/0rN6mBb.png)
- raw format image files dont have metadata
    - must validate manually
- in accessdata ftk imager, when selecting Expert Witness (.e01) or SMART (.s01) format,
    - extra options for validating acquisition available
    - validation report shows md5 and sha-1 hashes
---

## Data Hiding Techniques
---
###### Data Hiding
- changing/manipulating file to conceal info

###### Techniques
- hiding entire partitions
	- use disk management
- changing file exts
- setting file attributes to hidden
	- change file signature
- bit shifting
	- shift 1 bit to left
- use encryption
- password protection
---
#### Hiding Files using OS
- change file extensions
- tools check file headers
    - compare file extension to verify
    - if there's discrepancy, tool flags file as **possible altered file**
- other hiding technique by selecting hidden attribute in file's properties dialog box in windows
---
#### Hiding Partitions
- use windows `diskpart remove <letter>` command
    - can unassign partition's letter which hides it from file explorer
    - use `diskpart assign <letter>` to unhide
- other disk mannagement tools
    - partition magic
    - partition master
    - linux grand unified bootloader (GRUB)
- to detect whether partition hidden,
    - account for all disk space when examining drive
    - analyse all disk areas containing space u cannot account for
- in prodiscover, hidden partition appears as highest avail drive letter in BIOS
    - other tools have own methods to assign drive letters
---
#### Marking Bad Clusters
- data hiding technique in FAT is placing sensitive data in free/slack space on disk partition clusters
    - involve old utilities like norton diskedit
- can mark good clusters as bad so OS consider them unusable
    - only way to access by changing back to good cluster with disk editor
- diskedit runs only in ms-dos and can only access FAT-formatted disk media
---
#### Bit-Shifting
- some users use low level encryption program that changed order of binary data
    - makes altered data unreadable
        - to secure file, users run assembler program *(AKA macro)* to scramble bits
    - run another program to restore scrambled bits to original order
- bit shifting changes data from readable code to data that looks like binary exe code
- winhex includes bit shifting feature
---
## Steganography & Applications
---
###### steganography 
- greek word for hidden writing
- hiding msg where only the intended recipient knows its there 
- **applications:**
	- digital watermarking

###### steganalysis
- detecting and analysing steganography files

###### digital watermarking 
- a kind of marker secretly embedded in audio, video, or image data
- developed as way to protect and identify file ownership
    - only found under certain conditions (e.g. after using some algorithm)
    - usually not visible after using steganography
- **applications:** ^56429d
	- copyright protection
	- source tracking
		- each data is watermarked, and the watermark identifies the source of distribution

###### using steganography tools
- way to hide data is use stego tools
    - many are freeware/shareware
    - insert info into variety of files
- if encrypt plaintxt file with pgp and insert encrypted txt into stego file, cracking encryped msg is very dificult

###### steganalysis methods
- stego only atk
	- only have converted covered file to analyse
- known cover atk
	- has both covered file and converted covered file to analyse
- known msg atk
	- when hidden msg revealed ltr
- chosen stego atk
	- stego tool used
- chosen msg atk
	- steganalyst generates stego-obj from some stego tool/algo of chosen msg
---

## Examining Encrypted Files
---
- to decode encrypted file,
    - supply password/passphrase
- many encryption programs use tech called **key escrow**
    - designed to recover encrypted data if users forget password or if user key corrupted after system failure
- key sizes of 2048bits to 4096bits make breaking them impossible with current tech
- OR try to make suspect reveal encryption passphrase
---

## Recovering Passwords
---
- password cracking tools available for handling password protected data
    - some integrated into tools
- standalone tools
    - last bit
    - accessdata prtk
    - ophcrack
    - john the ripper
    - passware
---
###### brute force attacks
- use every possible letter, number, and char
- need a lot of time and processing power
- OS and application store passwords in the form of MD5 or SHA hash values
	- brute force attacks require converting dict pwd from plaintxt to hash val
		- needs more cpu cycle time

###### dictionary attack
- use common words in dict
- use variety of langs
- many programs can build profiles of suspect to determine password

###### rainbow table
- file containing hash values for every possible password generated
- no conversion needed
	- faster than brute force/dict atk

###### salting passwords
- make password cracking difficult
- alter hash values with extra bits added to password
---

## Summary
---
![](https://i.imgur.com/bhy1teA.png)
![](https://i.imgur.com/9fdjpIR.png)
![](https://i.imgur.com/eUjn8MS.png)
