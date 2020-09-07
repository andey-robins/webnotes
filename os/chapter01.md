Chapter 1
=====
This will be a huge overview of everything with very little depth.

## What is an Operating System?
An OS is the intermediary program between a user and the computer's hardware.

"An operating system is a program that controls and coordinates the use of hardware resources among various programs for various users." - The textbook

Unfortunately, there is no universally accepted definition.

Goals:
- execute user programs
- make the system convenient
- use hardware efficiently

### Function of Operating Systems
Users -> Ease of use and good performance, but often don't care about5 resource utilization
Shared computers (mainframes or minicomputers) -> need to keep all users happy
Handheld Computers -> resource poor because they're optimized for usability and battery life

## System Structure
1. Hardware - basic computing
2. Operating System
3. Application Programs - defines how system resources are used to solve problems
4. Users - users or other computers

### Multiprogramming (Batch Systems)
Began to re-gain popularity in the high performance area.
- single user can't keep I/O and CPU busy at the same time
- multiprogramming organizes jobs so that one program takes over the CPU when another is doing I/O
- do do this, we use a job scheduler
    - determines what's next
    - a very very tiny piece of code
    - most important part of the computer you don't know exists

### Timesharing (multitasking)
Switching jobs so frequently that user's feel they're the only one using the computer.
- response time of < 1 second
- moving memory around

## OS Operations
Operations are interrupt driven, whether in hardware or software. 

Dual-mode operations allow the OS to protect itself and its components.
- user mode and kernel mode
- mode bit is provided by hardware
    - bit set to determine when sytem or user code is running
    - some instructions are only possible in kernel mode
    - system call changes mode to kernel

### Process Management
- a program is a passive entity
    - compiled code sitting on a hard drive
- the process is an active entity
    - the actively running code and all the resources needed for execution
    - when a process starts and stops the OS needs to manage all those resources
- process management is responsible for:
    - creation
    - deletion
    - suspension
    - resuming
    - synchronization
    - communication
    - deadlock

### Memory Management
- the program has to actually be moved into memory in order to be used

### Storage Management
- this class will have the abstract concept of a file
    - a file stores data
- we must conceptualize file management
    - how and where do we put stuff
    - how do we create and delete them
    - how do we find them
    - etc.
- where is short term storage and where is long term storage?
- levels fast access -> long access; also small size -> big size:
    - 1 - registers
    - 2 - cache
    - 3 - main memory
    - 4 - solid state
    - 5 - magnetic disk

### Protection and Security
- protection -> any mechanism to control access to process or users
- security -> defence of the system against attack
- a lock is protection, whether you lock it is security

### Kernel Data Structures
- singly linked lists
- doubly linked lists
- circular linked lists
- binary search trees
- hash maps
- bitmap

## Computing Environments
- stand alone general purpose computer
- portal
    - web access to internal system
- network computers (thin clients)
    - web terminals
    - all of the work in the backend/cloud
    - chromebooks, etc.
- mobile computers
- distributed computing
    - usually creates the illusion of one machine
    - connected via the network
- client server model
    - server returns interface and requests
    - could be a file-directory type system
    - replaces the computer with a way to connect to the network and then have the server do it
- peer-to-peer networks
    - distributed storage model
    - all are clients & all are servers
    - napster, gnutella, skype
- virtuals
    - the environment is created by an underlying environment
    - emulation
- cloud computer
    - "very very not here"
    - functionality as a service
    - the next level of virtualization
- real time embedded systems
    - what controls cars, etc.
    - missing something is a catastrophic failure

## Final Takeaway
1. OS depends on the architecture
    - processors
    - hardware
    - bus
    - etc.
2. OS depends on application
    - what applications to use
    - where will it be running?
    - what does it need to do?

### Process
A program in execution (the active part of the program).

An OS must be able to create, run, store, and kill a process.