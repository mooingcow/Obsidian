
# 09 Cellular Mobile Networks
---

## How do Cellphones Work?
---
###### mode of communication
- full duplex
	- 2 channels
	- speak and listen at same time
	- cell phones essentially 2 way radio
		- radio transmitter & radio receiver
		- phone converts voice into electrical signal then transmit via radio waves to nearest cell tower
- half duplex
	- cb radios (citizen band)
		- radio freq signal <-> electrical signal
	- only one speak at a time
	- eg. walkie talkie
- use radio waves to talk to cell tower that connects it to rest of phone network

###### cellular layout
- phone network composed of **cell** or signal area
    - cells overlap or join to form large coverage area
    - users on network can cross into diff cells w/o losing connection
- phone networks allows for **frequency reuse**
    - below, cell 1s on same frequency but wont interfere due to physical separation
    - inteference called **crosstalk**

![](https://i.imgur.com/AuyomC7.png)

###### cellular division
- cellular device can communicate with another
- cells in hex shapes
    - preferred than square or circle as covers entire area w/o overlapping

![](https://i.imgur.com/V83sOAF.png)

###### cell antennas
![](https://i.imgur.com/hbydZSD.jpg)
![](https://i.imgur.com/EQS8uO6.jpg)

###### find towers
![](https://i.imgur.com/ahEOUeq.png)
- http://www.cellreception.com/towers
---

## Data Transmission in Mobile Networks
---
###### MTSO
- mobile telephone switching office (mtso)
    - contains switching equipment for routing mobile phone calls 
    - handles entire cell network
    - controls **handoff**
        - process of transferring ongoing call or data session from one channel (cell) to another channel (cell)
    - comm with PSTN (public switch telephone network)
        - landline network
    - brain of cell phone network
- mtso evaluates signal strength between device and network
    - tell device/network to make appropriate adjustments to transmission

![](https://i.imgur.com/4JokKd1.png)

###### how data is transmitted
![](https://i.imgur.com/f4k3Rkb.png)


###### wireless frequency
- transmission of voice or data through use of electric waves set to specific frequencies
    - number of waves per second = freq
    - freq measured in hz
    - 1 hz = 1 complete wave length per sec

![](https://i.imgur.com/inLnLny.png)

###### what happens...
- when phone turns on

![](https://i.imgur.com/dO7HPpi.png)

- when place call
![](https://i.imgur.com/aHuvZo4.png)


###### cellular hand-off
- if signal on channel from tower weakens during a call, another tower and handoff needed
    - if no other tower with stronger signal, call dropped

![](https://i.imgur.com/FEf32Jr.png)

###### hard vs soft hand-off
| Hard | Soft |
| -- | -- |
| Existing connection must be broken before new connection can be formed<br/><br/>Break then make | New connection is established before old connection is broken<br/><br/>Make before break |
| Allocates different frequency | Allocates same frequency |
| Communicates with one base station at a time | Communicates with 3-4 base stations at the same time |

![](https://i.imgur.com/RxUK5i1.png)

---

## Cellular Subsets
---
###### access technologies
- how phone talks to tower:
    - AMPS (advanced mobile phone system)
        - FDMA
        - 800 MHz
        - 1G
        - analog
    - TDMA (time division multiple access)
        - 2G
        - digital
    - iDEN (integrated digital enhanced network)
        - 2G
        - digital
    - CDMA (code division multiple access)
        - 2G/3G
        - digital
    - GSM (global system mobile communication)
        - 2G
        - digital
    - W-CDMA (wideband CDMA)
        - 3G
        - digital
    - OFDM (orthogonal frequency-division multiple access)
        - 4G
        - digital
---
###### TDMA
- time division multiple access
    - method of digitizing and compressing
    - num of equal timeslots configured for each frequency channel
    - divides convos by freq and time
    - outdated tech
- facilitates many users to share same frequency w/o interference
    - divides signal into diff timeslots and increases data carrying capacity
- breaks up frequency allocation by time
    - eg. 6.7ms
- 2 channels used
    - decoding
    - encoding
---
###### iDEN
- integrated digital enhanced network
    - based on TDMA
- iden phones can support sms messages, voice mail, and data networking eg. vpn, internet and intranets
- allow users to take advantage of **PTT (push to talk)** walkie talkie tech
    - half duplex
    - used by
        - sprint
            - shutdown in 2013
        - at&t
        - verizon
---
###### CDMA
- code division multiple access
- uses spread spectrum tech
    - spreads info contained in particular signal of interest over greater bandwidth than original signal
- assigns code to each piece of data passed across spectrum
- newer tech still uses orig tdma concept
    - deemed more superior to fdma and tdma
- cannot carry voice and data at same time
- every communication channel uses full available spectrum
- 2 channels
    - encoding
    - decoding
- spread spectrum
    - channels spread across entire freq range instead of 1 dedicated one
        - 1850 mhz - 1990 mhz

![](https://i.imgur.com/FxQ9rBc.png)

##### CDMA Family
- cdmaOne (2G)
    - orignal cdma system
- cdma2000 (3G)
    - evolved from cdmaOne
    - family of tech for 3G cellular communication for transmission of voice, data and signals
    - 1xRTT (voice), 1xEV-DO (3g wireless standard data)
- W-CDMA (3G)
    - borrows ideas from cdma
    - use gsm tech and evolve into UMTS (universal mobile telecomms service)

##### BitPIM Software for CDMA
- open source cross platform that allows u to view and manipulate data on many cdma phones
    - include phonebook, calendar, wallpapers, ringtones and filesystem
- analyse most qualcomm cdma chipset based phones
- PIM = personal info management

##### Qualcomm for CDMA
- founded in 1985 by multinational semiconductor and telecomms equipment company
    - created CDMA and components in 1990s
    - orignally built base stations, chipsets and phones
    - owns patent on CDMA chipset tech
---
###### GSM
- based on TDMA
    - 70%-80% of phones
- digital cellular tech for transmitting mobile voice and data services
- established in 1987 as standard
    - avail in >212 countries
- global systems for mobile communication with freq 850-1900mhz
- uses SIM tech

![](https://i.imgur.com/A06ytH5.png)

---

## Cell Phone Identification Numbers
---
###### Mobile Identity Number (MIN)
- 10 digit
    - more with country code
    - assigned by carrier & used for phone identification
    - eg. (303)866-1010
- 2 parts
    - MIN 1
        - 24 bit number after area code
    - MIN 2
        - area/mobile subscriber code
- can be ported
---
###### Electrical Serial Number (ESN)
- unique 32bit number assigned to each TDMA or CDMA (non GSM) device
    - like mac address
- uses 14 bit code for manufacturer code
    - since 8bit almost exhausted

![](https://i.imgur.com/uEe03md.png)

---
###### Mobile Equipment ID (MEID)
- replace soon exhausted ESN for CDMA devices
- all fields are hex values
    - **RR**
        - regional code
        - global administered
    - **XXXXXX**
        - 000000 - for small quantities of test/prototype mobiles
        - 000001 - FFFFFE
            - reserved for regional admin bodies or mobile manufacturers
            - subject to industry agreement
		- FFFFFF
			- reserved
    - **ZZZZZZ** 
	    - manufacturer assigned to uniquely ID device
    - **C**
        - check digit
        - not tramistted over air

![](https://i.imgur.com/TpDbzgs.png)

---
###### International Mobile Equipment Identity (IMEI)
- unique 15 digit code to identify individual GSM mobile to mobile network
- displayed on phones by dialing code `*#06#`

| Field | Function|
|---|---|
| Type Approval Code (TAC) | Identifies country that type approval was sought and the approval number|
| Final Assembly Code (FAC) | Identifies company that produced handset |
| Serial Number (SNR) | Uniquely identifies specific type of handset |
| Check Digit (CD) | Check IMEI validity |

![](https://i.imgur.com/YcYttBd.png)
![](https://i.imgur.com/YASPtMQ.png)

##### IMEI Checksum Verification
- 3 steps
    - starting from right, double every other digit
    - sum digits
        - note that 14 is 1 + 4 not +14
        - check if sum is divisible by 10

![](https://i.imgur.com/yXmtnzg.png)

![](https://i.imgur.com/FeWVvfn.png)

---
###### International Mobile Subscriber Identity (IMSI)
- global unique identifier
- 56 bit
    - unique in every network
- allowed for authentication of device to network
- 3 parts
    - **MCC**
        - mobile country code
        - 3 digits
        - all MCC is assigned by ITU (internation telecomm union) 
	        - in recommendation E.212 (internaitonal identification plan for public networks)
    - **MNC**
        - mobile network code
        - 2 digits
    - **MSIN**
        - mobile station identification number
        - 10 digits

![](https://i.imgur.com/ja3PXES.png)
![](https://i.imgur.com/S1sUv1N.png)

---
