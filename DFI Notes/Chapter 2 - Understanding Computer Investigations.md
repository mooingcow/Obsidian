
# 02 Understanding Digital Forensics
---

## Systematic Approach
---
![](https://i.imgur.com/EEfwoNK.png)

#### Steps for problem solving
1. make initial assessment about case type
	- eg. interview ppl, places to visit etc.
2. determine preliminary design/approach to case
	- eg. when to visit company employees
3. create detailed checklist
	- stay on track
4. determine resources needed
5. obtain copy of of evidence drive
6. identify risks
7. mitigate/minimise risks
	- ensure evidence always available
8. test design
9. analyse and recover digital evidence
10. investigate data recovered
11. complete case report
12. critique case
	- self evaluation to improve


## Assessing Case
---
- outline case details including
    - situation
        - eg. employee abuse case
    - nature of case
        - eg. used email for personal stuff
    - specifics of case
        - eg. detailed info of case
    - type of evi
        - eg. usb drive
    - known disk format
        - eg. FAT
    - location of evi
        - eg. usb recovered from employee's desk


## Planning Investigation
---
#### Basic Investigation Plan
1. acquire evidence
2. **evidence form** and chain of custody ^efb39a
	- shows where file came from, who created it and type of equipment used
	-  maintain each record of the digital evidence from collection to presentation
3. transport evidence to computer forensics lab
4. secure evidence in **approved secure container**
5. prep for **forensics workstation**
6. retrieve evidence from secure container
	- ensure info confidential
	- container shld be locked, fireproof locker/cabinet with limited access
7. make forensic copy of evidence
8. return evidence to secure container
9. process copied evidence with computer forensics tools
	- Eg. Encase


### Evidence Forms
---
- evidence custody form helps document what has been done with original evidence and forensics copies
	- AKA **chain of evidence form**
- contains info such as:
	- model/serial num of computer component
	- evidence recovered by
	    - name of investigator
		    - chain of custody starts here - person with stated name is responsible for preserving, transporting and securing the evi
	- date and time that evidence is taken into custody

##### Single Evidence Form
- lists each evidence on a seperate page
- ![](https://i.imgur.com/tHynAoA.png)

##### Multi-Evidence Form
- lists multiple evidence on a single page
- ![](https://i.imgur.com/e6jgALd.png)


### Securing Evidence
---
- use **evidence bags** to secure and catalog evidence
- use computer safe products when collecting computer evidence
    - antistatic bags
    - antistatic pads
- use well padded containers
- use **evidence tape** to seal all openings
    - cd drive bays
    - insertion slots for power supply electrical cords and usb cables
    - write initials on tape to prove that evi not tampered with
- consider computer specific temperatures and humidity range
    - ensure have safe environment for transporting and storing until secure evidence container available



## Conducting an Investigation
---
- gather resource identified in investigation plan
- items needed
    - orignal storage media
    - evidence custody form
    - evidence container for storage media
    - bit stream imaging tool
    - forensics worktstation to copy and examine evidence
    - securable evidence locker/cabinet/safe


### Bit-Stream Copies
---
- bit stream copy
    - bit by bit copy of orignal storage medium
    - exact copy of original disk
    - different from simple backup copy
        - backup software only copy known files
        - backup software cannot copy deleted files, email msgs or recover file fragments
    - copy image file to target disk that matches orignal disk's manufacturer, size and model
- bit stream image
    - file containing bit stream copy of all data on disk/partition
	    - AKA image or image file

![](https://i.imgur.com/vquuMJR.png)

#### Acquiring Image of Evidence Media
- 1st rule of comp forensics - preserve orignal evidence
- conduct analysis only on copy of data
- several vendors provide MS-DOS, linux and windows acquisition tools
    - windows tools require write-blocking device when acquiring data from **FAT or NTFS** file systems


## Completing Case
---
- produce final report
    - state wha u did and what u found
- repeatable findings
    - repeat steps and produce same result
- if required, use report template
    - report shld show conclusive evi
        - suspect did/did not commit crime or violate company policy
- keep written journal of everything you do
    - notes can be used in court
- answer the 6 Ws
    - who what when where why and how
- must explain computer and network processes
    - good to identify who your report reader is and write something suitable for reader


## Critique Case
---
- ask these qns
    - how to improve performance in case
    - got expected results? did case develop in ways you didnt expect?
    - is documentation thorough enough?
    - what feedback received from requesting src?
    - discover any new probs?
    - used new techniques during case/research?



## Private Sector High-Tech Investigations (Examples)
---
- need to develop formal procedures and informal checklists
    - cover all issues important to high tech investigations
    - ensure correct techniques used in investigations
    - diff cases may have different procedures
---
#### Employee Termination Cases
- majority of investigative work for termination involves employee abuse of corporate assets
- incidents that create hostile work environment are predominant types of cases investigated
    - viewing porn in workplace
    - sending inappropriate emails
- orgs must have appropriate policies in place
    - consult hr dept
---
#### Internet Abuse Investigations
- need
    - org's internet proxy server logs
    - suspect computer's ip address
    - suspect computer's disk drive
    - preferred computer forensics analysis tool
- recommended steps
    - use standard forensic analysis techniques and procedures
    - use appropriate tools to extract all webpage url info
    - contact network firewall admin and request proxy server log
    - compare data recovered from analysis to proxy server log
    - continue analysing computer's disk drive data
---
#### Email Abuse Investigations
- need
    - electronic copy of offending email with msg header data
    - if available, email server log records
    - for email systems that store user's msgs on central server, access to server
    - access to comp so can perform forensic analysis on it
    - preferred forensics tool
- recommended steps
    - use standard techniques
    - obtain electronic copy of suspect's and victim's email folder/data
    - for web-based email investigation, use tools like FTK'S internet keyword search option to extract related email address info
    - examine header data of all messages of interest to investigation
---
#### Industrial Espionage Investigations
- all suspected cases should be treated as criminal investigations
- staff needed include:
    - **computing investigator**
        - resp for disk forensics examinations
    - **tech specialist**
        - knowledgable of suspected compromised technical data
    - **network specialist**
        - can perform log analysis and setup network sniffers
    - **threat assessment specialist**
        - typically an attorney
- guidelines for investigation
    - determine if investigation involves industrial espionage incident
    - consult corporate attorneys and upper management
    - determine what info needed to substantiate investigation
    - generate list of keywords for disk forensics and sniffer monitoring
    - list and collect resources needed
    - determine goal and scope of investigation
    - initiate investigation after approval from management
- planning considerations
    - examine all email of suspected employees
    - search internet newsgrps or msg boards
    - initiate physical surveillance
    - examine facility physical access logs for sensitive areas
    - determine suspect location in relation to vuln asset
    - study suspect's work habits
    - collect all incoming and outgoing phone logs
- steps for inves
    - gather all personnel assigned to investigation and brief on plan
    - gather resources for investigation
    - place surveillance systems at key locations
    - discreetly gather extra evidence
    - collect all log data from networks and email servers
    - report regularly to management and corporate attorneys
    - review investigation's scope with management and corporate attorneys
---
#### Interviews and Interrogations in High-Tech Investigations
---
- becoming skilled interviewer and interrogator can take many years of exp
- definitions
    - interview - usually conducted to collect info from witness/suspect
        - about specific facts related to investigation
    - interrogation - process of trying to get suspect to confess
- computing investigator role
    - instruct investigator on what qns to ask and what answers shld be
- ingredients for successful interview/interrogation
    - patience throughout session
    - repeating/rephrasing qns to zero in on specific facts from reluctant witness/suspect
    - being tenacious
---

## Data Recovery Workstations and Software
---
- inves conducted in comp forensics lab/data recovery lab
    - in data recovery, client just wants data back
- computer forensics workstation
    - specially configured pc
    - loaded with extra bays and forensics software
- to avoid altering evi use **write-blocker devices**
    - enable u to boot windows w/o writing data to evi drive

### Setting Up Workstation for Digital Forensics
- basic requirements
    - workstation running win xp or later
    - write-blocker device
        - prevent writes to storage devices
    - digital forensics acquisition tool
    - digital forensics analysis tool
    - target drive to receive src or suspect disk data
    - spare PATA (parallel) or SATA (serial) ports
    - usb ports
- extra useful items
    - nic
    - extra usb ports
    - firewire 400/800 ports
    - SCSI card
    - disk editor tool
    - txt editor tool
    - graphics viewer program
    - other specialised viewing tools

### Acquiring File Evidence with ProDiscover
---
#### Acquire USB Drive
- use prodicsover basic to acquire usb drive
    - create work folder for data storage
- steps
    - on usb drive locate write-protect switch and place drive in wirte-protect mode
    - start prodiscover basic
    - in main windows, action > capture image from menu
    - click src drive drop down list and select thumbdrive
    - click >> btn next to dst txt box
    - type name in technician name txt box
    - prodiscover basic acquires an image of the usb drive
    - click ok in completion msg box

![](https://i.imgur.com/3D5Sz1C.png)
![](https://i.imgur.com/mcLEcTh.png)

#### Analysing Digital Evidence
- job to recover data from
    - deleted files
    - file fragments
    - complete files
- deleted files linger on disk until new data saved on same phy location
    - or reformat performed
- prodiscover basic can retrieve deleted files
- steps to analyse usb drive
    - start basic
    - create new case
    - type project num
    - add image file
- steps to display contents of acquired data
    - click expand content view
    - click all files under image filename path
    - click letter1 to view contents in data area
- analyse data - search for info related to complaint
- data analysis can be most time-consuming task

![](https://i.imgur.com/cj1kr8G.png)
- prodiscover basic can
    - search for keywords of interest in case
    - display results in search results window
    - click ea file in search results window and examine content in data area
    - export data to folder of your choice
    - search for specific filenames
    - generate report of activities

![](https://i.imgur.com/DQB6YOA.png)
![](https://i.imgur.com/PqQHaSI.png)
![](https://i.imgur.com/iDvxmSk.png)

#### Completing the Case
- produce final report
- include prodiscover report to document work
- everything similar to point above


## Summary
---
![](https://i.imgur.com/ktdiAz2.png)
![](https://i.imgur.com/jsO2lw8.png)
![](https://i.imgur.com/GoSKOge.png)
