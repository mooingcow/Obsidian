
# 11 iOS Forensics Part 1
---

## Seizure and Isolation
---
###### seizure
1. note location of mobile
2. take picture of the location
3. [[Chapter 2 - Understanding Computer Investigations#^efb39a|chain of custody]] 
4. take pictures of the crime scene before starting any progress
		- original state of the mobile device
		- brand
		- model
		- serial number
		- IMEI number or operating system version
5. request for passcode, SIM pin, iTunes backup password if possible
6. check for any Unified Endpoint Management solutions
7. note the status of the device
	- whether it’s powered off or on
	- if it is powered on then, check the battery status, network status
	- check where the screen is locked
8. search/request for the SIM and if any cables are located around

##### note:
- circumventing the passcode/iTunes backup password is not always possible
	- try to secure the passcode from the owner and/or immediately disable the passcode requirement if possible
	- Place the phone in “airplane mode”
	-  change auto-lock setting to “never” for duration of forensic acquisition
	- document settings changed prior to taking a forensic image
---
###### isolation techniques (on)
1. activate airplane mode
2. check and manually disable:
	- “hotspots” or any GPS locations
	- Wi-Fi and Bluetooth toggles
3. connect the phone to a power bank
4. do not remove the SIM
	- device may lock up when SIM is removed
5. use lightning adapter to prevent USB restricted mode from being activated 
	- for devices running iOS 11.4.1 only
	- iOS 12 and 13 may restrict USB immediately
6. place the phone, adapter, and charger into the Faraday bag (if possible)
---
###### isolation techniques (off)
**note:** do not turn on the device
1. place it in an evidence bag or box
2. place the phone, adapter, and charger into the Faraday bag (if possible)
3. bring it back to Forensic Lab
4. remove & do acquisition of the SIM card
5. if necessary to turn it on, apply the above isolation techniques
---
###### forensic acquisition
- the process of acquiring the original evidence while maintaining its integrity
	- AKA imaging
- can be done on-site (at the scene) or off-site (in the lab)
---
###### hashing
- done after acquisition of device
- used to prove the integrity of the evidence
- MD5 or SHA are widely used algorithms to calculate the hash values
- should be documented as well to maintain record of the digital evidence
---

## Types of Acquisition
---
![](https://i.imgur.com/80mJu3M.png)
___
###### advance logical
- combines both logical and file system extraction methods
---
###### cloud acquisition
- iCloud backups
- iCloud drive (full content, including third-party app data not available by any other means)
- iCloud photos
- FileVault2 recovery token (FileVault is a disk encryption program in Mac Operating system)
- iCloud keychain
- health data
- messages (iMessageand SMS)

##### disadvantages
- need proper authentication credentials
- need the user’s Apple ID and password
	- & two factor -authentication (if 2FA is enabled)
---
###### acquisition via iTunes backup
- if iOS device not available
	- backup can be retrieved from the workstation (Windows or MacOS)
- device typically connects for updates or syncing music, movies and applications
	- iTunes performs automated backup 
		- during the sync process
		- when an upgrade to the iOS is performed
- Backups are stored in alternate locations depending on the OS
![](https://i.imgur.com/9JYlG6N.png)
---
###### manual
- the examiner uses the UI of the phone to browse and investigate
- no special tools or techniques required
- manual extraction of chat messages 
	- screenshot 
	- export to external media
- **however**, only files and data visible through the normal UI can be found
- data extracted through other methods can be verified using this
- very easily to modify data on the device
---
###### brute force
 - offensive techniques: 
 - password, pattern, or pin cracking
 - rooting the device
---

## Operating Modes of iOS
---
###### operating modes
- normal mode
- recovery mode
- DFU mode
---
###### normal mode
- in normal mode, the user can perform all regular activities
- normal mode boot process consists of 3 steps:
	- low-level bootloader
	- iBook
	- iOS kernel
- these boot steps are signed to keep the integrity of the process
---
###### recovery mode
- during the normal boot process 
	- if any step is failed to load or verify
	- the device enters into recovery mode
---
###### DFU mode (Device Firmware Upgrade)
- used to perform IOS upgrading
	- a low-level mode for diagnosis
- during boot up, if Boot ROM is not getting a load or verify
	- then iPhone presents the Black screen
---

## Jailbreaking
---
- the process of exploiting the flaws of a locked-down device to install software other than what the manufacturer has made available for that device
- allows the device owner to gain full access to the root of the operating system and access all the features
	- gain access to all partitions including file system with read-write only permissions
- not accepted forensically because it may overwrite some important data but allows performing physical acquisition efficiently
- used when root access of the file system is required as well as for the physical acquisition

##### disadvantages
- Apple considers jailbreaking iOS to be a violation of its terms and conditions of use 
- jailbreaking exposes a phone to several risks, including:
	- security vulnerabilities
	- stability issues
	- potential crashes and freezes
	- shortened battery life
---

# iOS Forensics Part 2
---

## iOS Devices
---
###### iPhone
- most popular among IOS devices
- due to design, camera and features

###### iPad
- apple launched iPad tablet known as iPad or iPad first Generation
- released after the iPhone 3Gs

###### iPod
- first iPod was launched by Apple in 2001
	- known as “First Generation”
- subsequent have been referred as “Second Generation” and so on
- initially launched as music player
	- advanced to have the ability to play videos and games to users
- an examiner could retrieve forensic data from storage, browser, gallery, etc. on an iPod
- iPod Touch models featured
	- camera, Wi-Fi Capabilities, safari web browser, storage and playback for audio, video and photo, YouTube player
	- apps could be installed from app store
---

## iOS Architecture
---
###### operating system
- both the Mac OS X and iOS evolved from an earlier Apple operating system called Darwin
	- Darwin is a Berkeley Software Distribution (BSD) Unix OS
	- it is a discontinued operating system based on Research Unix
- iOS is a proprietary mobile operating system owned by Apple and it is only allowed to be installed in Apple equipment or devices
- mobile operating systems such as Android and iOS are based on Unix-like operating systems
- linux is a family of open-source Unix-like operating systems

![](https://i.imgur.com/AwcpFVM.png)
___
###### sandboxing
- a technology for security and control
- enforces a strict set of rules 
	- which apps can be installed on a device 
	- exactly what they can do
	- minimum set of privileges it needs to get its job done

###### standard directories
![](https://i.imgur.com/cWEpmoN.png)
___

## iOS File System
---
###### hierarchical file system (HFS+)
- provides large data sets
- disk formatted with HFS has 512-byte Blocks at physical level
	- 2 types of Blocks 
		- logical blocks
			- which are numbered from first to last within the volume
		- allocation blocks 
			- a group of logical blocks used to track data
			- can be tied together as groups to be utilised more efficiently by HFS
- uses both absolute time (Local time) as well as UNIX time so one can identify the location of the system.
	- absolute time 
		- e.g. 371589010
		- found in History.plist(safari)
	- UNIX time
		- e.g. 1349896210
		- found in moz_cookies(firefox), global_history.dat (opera)
- HFS files system uses catalog file system to organise data
	- uses B * tree (balanced tree) structure to organise data
		- trees are consists of nodes
	- when data is added or deleted, it runs the algorithm to keep balance

###### structure
- **reserved boot block**
	- first 1024 bytes are reserved boot blocks
- **volume header**
	- contains information about the structure of HFS Volume
	- keeps track of CatalogID numbering and increases it one each time file added
	- HFS+ volume header also contains signature “H+.”
- **allocation file**
	- keeps track of allocation blocks used by the file system
		- includes a bitmap
	- each bit represents the status of the allocation block
		- if it is set to 1
			- that means Allocation block is used
		- if it is 0
			- that means allocation block is not used
- **extent overflow file**
	- consists of a pointer to the extent of the file
	- if the file is larger than eight continuous allocation blocks, then it uses extents
- **catalog file**
	- organises data using balanced tree system
	- to find the location of file or folder within the volume
	- also contains the metadata of file 
		- creation and modification date
		- permissions.
- **attribute file**
	- contains the customisable attributes of a file
- **startup file**
	- assists the booting system which does not have built-in ROM support.
	- actual data is stored and tracked by the file system.
- **alternate volume header**
	- back up volume header located at last 1024 byte of the volume
- Last 512 Bytes are **reserved**

![](https://i.imgur.com/7eB5mMw.png)
___

## Partitions
---
###### system partition
- firmware/OS partitions
- read only partition
- containing only system files, upgrade files and basic applications

###### data partition
- contains user data
- will be the focus of most Investigation
- it is Read/Write partition
- where all iTunes applications will reside along with the user’s profile data

![](https://i.imgur.com/unyYuVa.png)
___

## File Types
---
###### property list (Plist)
- a data file used to store various types of data on iOS and Macintosh operating systems.
	- AKA property file
- originally Apple used the NeXSTEPformat or a binary format
	- was deprecated 
	- a new XML format was introduced
- property lists/XML files are used in the management of configuration of OS and applications
- contains useful artifacts
	- web cookies
	- email accounts
	- GPS map routes and searches
	- system configuration preferences
	- browsing history
	- bookmarks
- can be opened with a text editor to view the contents
---
###### SQLite databases
- SQLite data format is popular for mobile devices and open source applications
- logical extraction of the iPhone could provide lots of SQLite database files
- iOS uses SQLite databases to store user data, 
	- the tool SQLite browser is used to read SQLite database
	- can be downloaded from http://sqlitebrowser.org/
- native iOS applications utilise this database structure to store and organise their data
	- calendar
	- text messages
	- notes
	- photosa
	- address book
---
###### exchangeable image file (EXIF) metadata
- specifies the formats for images & sounds
	- used by digital cameras, scanners and other systems handling images
	- and digital cameras or voice recorders recording sound files
-  depending on the device used to capture, it contains
	- timestamps
	- longitude & latitude
	- location
	- device information
---

## Data Structure and Artifacts
---
###### timestamps
- iOS device will have many SQLite and plist files that can build a case for a forensic examiner
- iOS provides MACB (modified, accessed, changed, born date) times and can be vital when used with a timeline
- The Apple Core Foundation Absolute Time (CFAbsoluteTime) is also known as Mac Absolute Time or Apple Cocoa Core Data Time.
	- Timestamp e.g1615775963
	- https://www.epochconverter.com/
	- or Dcode(https://www.digital-detective.net/dcode/)
---
###### applications
- default applications store data in **private/var/mobile/Library**
	- address book
	- mail
	- calendar
	- maps
	- notes
	- YouTube
	- safari
	- messages
	- weather 
	- voicemail
- downloaded applications stored user data in **/private/var/mobile/** or **/User/**
	- e.g. */private/var/mobile/Application* or */User/Application*
		- this directory holds the files associated with each application
		- assigned a 32 character alphanumeric universally unique identifier (UUID) by Apple
			- e.g. /User/Applications/GA07A3WW-0E39-33OJ-B947-9CAA16688G22)
		- unique ID will be consistent across all iOS devices
---
###### iTunes backup
- inside the backup folder, there are several files that will tell the examiner if he is reviewing the correct iOS device
- the root of the backup folder will contain the status, info, and manifest plist files

##### status.plist
- provides data about the latest backup
- consists fields:
	- IsFullBackup: identifies whether the backup was a full backup of the device
	- UUID: Universally Unique Identifier (UUID) of the device
	- Date:  timestamp of the last time the backup was modified
	- BackupState: identifies whether backup is a new backup or one that has been updated
	- SnapshotState: identifies whether backup process has successfully finished

##### info.plist
- contains data to confirm the backup matches the device
- IMEI number can be found here along with the phone number

##### manifest.plist
- contains metadata about the backed up files
---
###### photos
- in **private/var/mobile/media/DCIM**
- contain photos either taken or synced to the device
- pictures found here will have timestamp metadata
- photos within the **100APPLE** folder indicate that they were taken from the device itself
- camera application numbers the images from the iOS device sequentially
	- first picture taken will be named IMG_0001 and will continue numbering 
	- without regard to files being deleted or moved
---
###### keystrokes
- in **/private/var/mobile/Library/Keyboard**
- dynamic dictionary is the text file **dynamic-text.dat**
	- stores words typed by the user during the course of using the device
	- any word entered into applications that allow text input will be captured
- to aid user in typing 
	- captures technical or special keywords that may not be Standard English words or acronyms 
	- could be helpful for the investigation
---
###### passwords
- in **/private/var/Keychains**
	- contains key-chain-2.db file
- iOS applications use Apple’s keychain for password management
- accounts and passwords can be found inside this database
	- voicemail passwords
	- wireless access point key phrases
	- device login passcodes
- passwords may be encrypted by iOS encryption keychain procedure
	- will need 3rd party tools to be decrypted
---
###### notes
- in **/private/var/mobile/Library/Notes**
- review acronyms or keywords that may be useful to investigation
---
###### text messages
- in **/private/var/mobile/Library/SMS** 
- review text messaging communication
---
###### browser cookies
- in **/private/var/mobile/Library**
- can be an important piece of evidence when identifying web browsing activities from the device
---
###### browser cache
- in **/private/var/mobile/Library/Caches/Safari**
- search terms can be found in **RecentSearches.plist**
---
###### addressbook
- in **/private/var/mobile/Library/AddressBook**
- AddressBook.sqlitedb file contain information about the owner’s personal contacts
---
###### call history
- in **/private/var/Library/CallHistory**
- call history is contained in call_history.db
---
###### geographical location and Wi-Fi data
- in /private/var/Library/Caches/locationd
	- consolidated.db 
		- wifilocationtable contains longitude, latitude, MAC, and timestamps of wireless infrastructures utilised
		- cellLocationLocaltable contains longitude, latitude, altitude, timestamps and tower data
- GPS and Wi-Fi evidence is a sought after item to help build a picture of the iOS device location at a specific time and also users habits
- many iOS applications will attempt to cache the user’s location and store GPS data 
	- e.g. iPhone’s camera will attempt to store longitude and latitude when a photo is taken
---
