Networking
=====

Class notes from Computer Science 4760, Computer Networking at the University of Wyoming. I took this class, and these notes, during the fall Semester of 2019.
There is no code associated with this class.

Routing Protocols
-----

Goal is to find least cost path
Basically just a graph traversal problem

###Static Routing
- Human caused changes
- Slow routing updates
- Not many required

###Dynamic Routing
- Changes as conditions change
- common with the prevalence of wireless technology
- Load sensitivity
    - trying to adjust based on load has historically been a problem
    - could cause network outages

###Link State
The network topology exists, but we don't know what it is.
Every node broadcasts its information to all other nodes
Uses Dijkstra's Algorithm for traversal
Also called Least-Cost algorithm
Can have oscillations because link costs are not asymmetric
    - asymmetric costs = different costs for both paths on a route
_O(V^2)_ -> less if the network is sparse
Expensive in terms of computation
    - since it is generally only run on sparse systems, the expense is mostly avoided

###Distance Vector
Only contacts immediate neighbors
Shares these vectors of connections to develop the path
Requires no synchronization
Not as fast since it's distributed
_O(VE)_
Uses Bellman-Ford algorithm
    - "fixed" Dijkstra's
    - Detects negative weight cycles

###Autonomous systems
An AS is a network under one administrative control
All routers run the same algorithm
Connected through a gateway router

###RIP
An intra-AS routing protocol
Uses UDP and a DV algorithm
Can have up to 25 routes -> not a very large network
Unable to do authentication (v1)
    - v2 fixed those issues
Not set up for IPv6
Low tier ISP and enterprise networks

###OSPF
Open Shortest Path First
    - open source
Uses LS
Admin sets link weights
Secure and can be authenticated
Upper tier ISPs
