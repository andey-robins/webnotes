Deadlock
=====
A set of blocked processes each holding each other up since they require each others resources.

What are our options? don't ever let the system enter a deadlock area; allow it to enter deadlock, detect it, and then recover; or ignore it

## Characterization
0. Deadlock happens when all 4 occur, to get rid of it, eliminate one of these things
1. Mutual exclusion: only one process can use a resource.
2. Hold and Wait: a process holding a resource and waiting for another
3. No preemption: a resource can only be released voluntarily by a process
4. Circullar wait: a process is waiting for resources held by another around and around

## Resource-Allocation Graph
- vertices and edges
- processes (round) and resources with the number of resources (nested squares)
- just because there's a cycle doesn't mean there will be deadlock, but it's only a strong possibility
- if no cycles, guarantee there is no deadlock
- only one instance per resource type, then deadlock
- multiple instances, possibility of deadlock

## Deadlock Avoidance
- require the system to tell us everything
- gets the total number of resources that will be required
- can figure out sequencing to avoid deadlocking
- leads to the idea of a safe state

### Safe State
- all processes can request everything they need in an order that will avoid deadlock
- single instance of resources uses a simple resource graph
- multiple instances uses a bankers algorithm

### Banker's Algorithm
- multiple instances
- each process claims a maximum use
- generates multiple data structures
    - Available: vector of available resources
    - Max: matrix that tracks all resources a process will request
    - Allocation: matrix that tracks all resources allocated to a process
    - Need: difference between allocation and max
- finds a possible path through all the processes that will ensure the system is always in a safe state
- after a request for resources, then run the algorithm again to see if it would still be in a safe state after giving those resources