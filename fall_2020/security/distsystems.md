Distributed Systems
-----
"You know you have a distributed system when the crash of a computer you've never heard of stops you from getting any work done" - Leslie Lamport

## Concurrency
- ultimately an ordering of operations even with many things happening at once
- understanding what state the data is in is a big part of it
- concurrent programming is very difficult
    - especially if there is some malicious agent within them
- eliminating security problems is incredibly difficult if not impossible
- time is ultimately the most complex problem of concurrency

### System Design Goals
- everything should be ACID
    - atomic (all or nothing)
    - consistent (transactions/actions balance)
    - isolated (serializable)
    - durable (actions cannot be undone)
- alternative
    - convergent -> if actions stop, the system will eventually reach a consistent state

## Fault Tolerance
- how are you going to create a system that can survive and recover from failure
- faults -> may cause an error
- error -> incorrect state
- failure -> deviation from correct behavior
- fault -> error -> failure
- faults and failures are a question of availability

### CIA Triad
- confidentiality -> no unauthorized reading
- integrity -> no unauthorized writing
- availability -> there when you want it

## Naming
- what do we call things
- there are ways to prevent two systems from interacting until trust is established
- uses things like SSL, passwords, kerberos, etc.
- if both entities don't trust each other, the ability to function can begin to degrade
    - we use redundancy to build up security on increasing layers

## Attacks on Distributed Systems
- replay attacks:
    - often a protocol issue
    - since there is likely some level of trust, can you exploit that to repeat some actions?
- race conditions:
    - usually a software issue