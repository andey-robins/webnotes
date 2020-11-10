Distributed Systems
=====
A distributed system is a collection of lososely copuled nodes interconnected by a communications network. Nodes could be processors, computers, machines, or hosts. The nodes could be client-server, p2p, or something else.

## Why Use Them
- resource sharing is the primary motivation
- speeds up computation through distribution
- increases reliability

## Networking
Largely a high level rehash of [networking](http://andey-robins.github.io/webnotes/mdwiki#!./fall_2019/networking.md).

## Networked OSes
- network os -> users are aware of the multiplicy of systems
- distributed os -> users are not aware of the multiplicity

## Distributed Coordination
In a distributed system there is no common time reference, so there is no way to guarantee one event happens before another.
How can we determine what happens before or after whatever?

### Solutions
- Have a centralized process dictating the ordering
- Fully distributed approach:
    - when a process wants to do a critical section, send its timestamp out to everyone
    - all other processes either respond or defer
    - when it receives a message from everyone else, it can go into the critical section
    - when it's done with the critical section, it replys to all defered messages
    - if two want to go into a critical section, it falls down to the timestamps sent out
- token passing

#### Problems with Fully Decentralized
- lots of messages going around
- each process must know all other processes
- overhead to see if processes fail
- each process must stop frequently to respond to messages

#### Problems with Token Passing
- if the token message disappears, then the system must "hold an election" to create the new token
- "talking stick" problem