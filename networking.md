Networking
=====

Class notes from Computer Science 4760, Computer Networking at the University of Wyoming. I took this class, and these notes, during the fall Semester of 2019.
There is no code associated with this class.

Routing Protocols
-----

Goal is to find least cost path
Basically just a graph traversal problem

###Static Routing
- human caused changes
- slow routing updates
- not many required

###Dynamic Routing
- changes as conditions change
- common with the prevalence of wireless technology
- load sensitivity
    - trying to adjust based on load has historically been a problem
    - could cause network outages

###Link State
the network topology exists, but we don't know what it is.
every node broadcasts its information to all other nodes
uses Dijkstra's Algorithm for traversal
also called Least-Cost algorithm
can have oscillations because link costs are not asymmetric

- asymmetric costs = different costs for both paths on a route

_O(V^2)_ -> less if the network is sparse
expensive in terms of computation

- since it is generally only run on sparse systems, the expense is mostly avoided

###Distance Vector
only contacts immediate neighbors
shares these vectors of connections to develop the path
requires no synchronization
not as fast since it's distributed
_O(VE)_
uses Bellman-Ford algorithm

- "fixed" Dijkstra's
- detects negative weight cycles

###Autonomous systems
an AS is a network under one administrative control
all routers run the same algorithm
connected through a gateway router

###RIP
an intra-AS routing protocol
uses UDP and a DV algorithm
can have up to 25 routes -> not a very large network
unable to do authentication (v1)

- v2 fixed those issues

not set up for IPv6
low tier ISP and enterprise networks

###OSPF
open Shortest Path First

- open source

uses LS
admin sets link weights
secure and can be authenticated
upper tier ISPs

Link Layer
-----

Physical connectors are the bomb right now; let's talk about that.

##Collision Issues

Assuming you can detect a collision, treat re-transmission similar to when you're talking with someone. If you both start talking at once, someone will restart after you both start. In computers, that time is random.

###ALOHA
- additive Links Online Hawaii Area
- sets up time slots using synchronization so that all devices can transmit on their slots
- transmit at the beginning of your slot
- if collisions occur, transmit on subsequent slots until you get through
    - use a probability *p* and transmit on a success
    - wait and try again on the next slot if not *p*
- 37% effective
    - original didn't have the synchronization part, so it was half as effective

###CSMA
- listen before you talk -> if it's busy, back off and don't interact
- one of the issues is the physical transmission time to move data around

###Taking Turns
- some algorithm basically "pings" you when it's your turn to transmit
    - Often some round robin algorithm
    - does allow for priority agents
- delay due to the polling and thinking done by the master agent
- bluetooth is a version of a polling share
- token passing
    - when you have the token, you can transmit
    - when you don't you can't talk

###Ethernet
- most common lan type today
- more on this later

###MAC Addressing
- physical address of the stuff
- assigned by IEEE not IANA
- assigned on manufacture
- unchangeable on older tech
- ARP - Address Resolution Protocol
    - basically DNS for MAC addresses
    - network address (usually IP) to 48 bit ethernet address (MAC address)
- only need to know your own MAC
    - send to broadcast channel (0*)

###My Day Off
Go through friday's slides since they had ethernet and switches

###VLAN
- a way to divide things up on a large switch
    - a 64 port switch might serve 3 "subnets" that you want to be unique
    - VLANs let you set up "smaller switches" within your big switch
- let you have programable networks
    - switch lets you isolate specific ports and set them up as a LAN across several switches
- VLAN frame modifications are added to move between VLANs
    - stripped off before the hosts see it
    - totally backwards compatible

###MPLS and Data Centers
- take notes from the book
- "Don't care" - Dr Buckner
- bitter about the data centers around laramie not being a thing and being petty with the university

Networking
-----
Note: we stop the exam material at chapter 6. This will not be on the second exam.

###Wireless Hosts
laptop
PDA
phone
many IOT devices
bluetooth
perhaps not even mobile hosts

###Wireless Links
Note: all wireless connections are considered to be on the edge of the network

- host and base station
    - base station usually a wired object
    - hosts always remain in contact with the base station
        - cell towers
        - wireless access points
    - hosts that are connected to a base are in infrastructure mode
        - part of the infrastructure of the network
    - connecting with each other but not the internet are *ad hoc*
        - must providing their own routing, address assignment, and DNS style service
    - a *handoff* is a mobile host moving from one association to another
- host and host
- operate under the assumption that everything above them remains the same
    - some services may change in ad hoc networks (i.e. DNS)

###Interference
- with physical connections (i.e. wires) the transmission medium has mild attenuation
- noise can be caused by electric issues around or damage to the transmission medium
- wireless interference is way more finicky
    - electricity rolling around everywhere causes noise in the environment that interferes with wireless communication
    - basic home appliances can cause interference with electricity
    - any form of electric surge can cause problems
    - building construction materials can scatter signal and turn it into noise
- pretty much impossible to determine why the signal is degraded
    - but can tell that it is
- measure a Signal-to-Noise ration (SNR)
    - value in dB
    - this is the ratio of the power of signal to the power of noise
    - *X * log_10 (received power/noise power)*
- also talk about BER (Bit Error Rate)
    - probability a bit will be received in error
    - inversely proportional to SNR
- can increase the SNR by increasing transmission power
    - problems with lots more power (duh)

###801.11
- single hop, infrastructure based
- nodes and a base station
- everybody has a MAC address
- access points have MAC addresses
    - they broadcast their SSID and MAC when someone comes into the network

###802.11
- uses CSMA/CA (collision avoidance) because we can't possibly detect collisions with all the noise
    - to do CD we would have to be able to monitor the network while transmitting
    - would have to transmit into the receiver
        - would destroy the receiver or simply over saturate it
    - makes detection impossible
- uses ARQ to acknowledge or retransmit

###CSMA/CA
1. sense channel. if it's clear then wait a DIFS. if still clear send frame
    - DIFS = distributed inter frame space. some random wait time
2. if busy, set a counter to random backoff and continue sensing. while its clear countdown.
3. when clear, send again
4. if ACK received -> GOTO step 1. else GOTO step 2 with a large backoff

###Hidden Terminal Problem
- problem of two terminals not being able to see each other
    - but they still share a single access point
    - can be caused by:
        - intervening structures
        - geography
        - fading
- solution is only an optional part of the communication protocol

###Bluetooth
- low power, short range, "cable replacement"
- originally interfered with wireless devices
    - added frequency hopping to prevent the issue (problem: 2.4 Ghz band is overused)
- ad hoc networks
    - operate as a "piconet"
        - a tiny network
    - 2 - 8 devices with one acting as a central hub
- primary devices are the one that you need to spend any sort of money on
    - creating bluetooth for a secondary device is trivial

###Zigbee
- similar to bluetooth
    - low power, low duty rate
- IoT devices like light switches, sensors, etc.

###WiMAX
- runs in parallel with wifi
- also allows wide area communications
- base station transmits
    - subscribers pick it up
- not a direct replacement for wifi
    - higher powered
    - requires some sort of client station
        - something like a powered dish/antenna

###Cellular Interent
- 1G systems, analog voice only
- 2G systems, voice only, digital replacement of 1G
- 2.5G systems added data
- 3G systems, voice and data, but the focus is speed
- 4G systems, IP based, "fully" deployed in 2011/2012
    - LTE is really only different in speed

Exam 2 Review
-----
Note: nothing from wireless is going to be on Exam 2

- Sections 4, 5, 6
- All lecture notes and homework answers online by Wednesday
- New format
    - multiple guess
    - fill in the blank
    - short answer (1-2 sentences)
- try not to assume things
- try not to overthink

###Chapter 4
- datagram networks
- IPv4
    - addressing
    - fragmentation
    - protocol
    - what's in the header and uses
- IPv6
    - addressing
    - fragmentation
    - header
- DHCP
- NAT

###Chapter 5
- ICMP
- routing algorithms
    - not in huge detail
    - both of them
        - what are they used for
        - when to use each
        - how do they update their data

###Chapter 6
- frames
    - CRC
- minimum frame size
- MAC addressing
    - how are they assigned
    - how are they used
- ARP
    - what is it used for
    - how does it work
- Ethernet topology
    - switches
    - hubs
    - busses
    - host arrangement
- CSMA/CD
    - what does it stand for
    - how does it work
- VLAN
    - why do it
    - how's it implemented

Cryptography
-----
###Definitions
plaintext - data to be encoded
ciphertext - encoded data
symmetric key - both parties have the same secret key
public/asymmetric key - public and private key system

####Vigenere Cipher
uses the square thing - monoalphabetic square
key word determines what column to pick from and plaintext determines row
vulnerable to the kasiski attack
frequency analysis attack

####Block Ciphers
1. divide input into fixed length blocks of bits
2. use a 1-to-1 map to convert to a new block
3. send new block
- *k* sized block has 2^(k)! possible maps
- effectively impossible for reasonably large data
- requires a blend between oversized data storage and computability and sufficiently large sizing

####Attacks
- statistical analysis
- known-plaintext Attack
    - Start with a known text string that might have been encoded and compare it to ciphertext
- chosen-plaintext attack
    - encode a known string and compare it to the ciphertext

####RSA
- choose *p* and *q* such that their product is 1024 bits
- n = pq and z = (p-1)(q-1)
- choose e < n that is relatively prime with z
- d is ed%z = 1
- public key (n, e)
- private key is (p, q)

DES is much faster, so we encrypt plaintext with DES and the key with RSA. Then transmit the key and the ciphertext before decrypting.

Authentication
-----

with hashing, we must find two strings that "must be computationally infeasible to find two strings such that their hash values are the same."
