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
=====

Physical connectors are the bomb right now; let's talk about that.

Collision Issues
-----
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
