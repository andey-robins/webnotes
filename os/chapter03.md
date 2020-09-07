Chapter Three -- Processes
=====
Without processes, there isn't a point to having a computer.

Process: A program in execution. Process execution must progress sequentially

## Process Concept
- Batch systems = jobs
- Time-shared systems = tasks
- job and process are almost interchangeable
- Parts:
    - The code (aka text section)
    - Program counter
    - Process registers
    - Stack
    - Data section (with global variables)
    - Heap (dynamically allocated memory during runtime)
- One program can be several processes
    - i.e. multiple users executing the same program

### Types of Process
- either os process (e.g. system call) or user process
- either I/O or CPU bound process
    - I/O bound: issues lots of I/O requests w/ little computation
    - CPU bound: uses CPU frequently and I/O infrequently
- independent or cooperating process
    - independent:
        - does not affect other process execution
        - is not affected by other processes
        - does not share data with other processes
    - cooperative
        - two or more processes
        - can affect other's execution
        - can be affected by other processes
        - shares data with other processes
- foreground or background process (minor)
    - foreground is holding onto a terminal w/ access to a user
    - background is detached and runs w/o user interaction

### Problems
- process scheduling - problem of when and which process to give the CPU to
- inter process communication:
    - mutual exclusion - if data is shared we might want to restrict one's access to avoid interference
    - process synch - if we want processes to reach a particular point at a specific time
    - deadlock - two or more processes waiting on resources that the others are holding
        - need to know when it happens and how to resolve it

### Process State
- new: being created
- running: instructions being executed
- waiting: waiting for something else to happen (e.g. I/O)
- ready: waiting on the CPU
- terminated: process has finished execution

### Process Control Block (PCB)
- what stores the information associated with the process
- state
- program counter
- CPU registers
- CPU scheduling info
    - priority
    - scheduling queue pointers
- memory-management info
- accounting information
    - CPU used
    - clock time elapsed
    - time limits
- I/O Status
    - devices allocated to it
    - list of open files

#### Threads
- so far a process has only had a single thread
- must have storage for thread details to put into the PCB

### Process Scheduling
- need to maximize CPU use (i.e. quicklly switch processes onto the CPU)
- the scheduler is the one who picks from available processes and puts one onto the CPU
- keeps scheduling queues of processes
    - job queue: set of all processes in the system
    - ready queue: set of all ready and waiting for execution
    - device queues: set of processes waiting for an I/O device

#### Schedulers
- short term scheduler (CPU scheduler)
    - selects which process should be executed next
    - probably the most executed program on a computer
- long term scheduler (job scheduler)
    - how many processes can be running
    - doesn't run very often
    - wants a good mix between I/O bound and CPU bound
- medium scheduler
    - deals with memory
    - brings stuff in and out of swap space

### Context Switching
- saves the state of the current process and then loads the new process
- context switching time is overhead since no useful work happens during the switch

### Process Creation
- a parent process creates children process
    - there's always a tree of processes
- the process gets a process identified (pid)
- resource sharing:
    - parent and children share resources
    - children share a subset of parents
    - no shared resources
- execution options:
    - parent and children execute concurrently
    - parent waits for child to die

#### Process of Process Creation
- child duplicate of parent
- child has a program loaded into ti
- `fork()` makes a new process that's a duplicate of the parent
- `exec()` is called right after a fork and loads a new program

### Process Termination
- make the `exit()` sys call
- return the status to the parent
    - parent is required to wait until receiving that
    - a parent may terminate a child with `abort()`

## Multiprocess Architecture
- Chrome Browser:
    - a single process used to be run for the entire web browser
    - chrome changed that by spawning multiple processes (one for each tab)
        - also has processes for IO, rendering, HTML, javascript, plug ins, etc. creating a bunch of processes.

## Interprocess Communication
- cooperating processes will need to share data somehow
    - independent processes don't interact with each other at all
- reasons/advantages:
    - info sharing
    - computing speedup
    - modularity
    - convenience
- we do this through IPC (interprocess communication)
    - shared memory (they all share a chunk of memory and let the processes do whatever they need there)
    - message passing (the OS will hand the message between the two)

### Producer-Consumer Problem
- evolves from IPC
- producers: create information
- consumers: consume the information created by a producer
- can be done with unbounded or bounded buffer
    - unbounded: no limit on the size of the buffer (or how much the producer can produce)
    - bounded: assumes a fixed buffer size (the producer can only produce so much before it has to wait on the consumer to consume it)

### Message Passing
- effectively emulates a network model
- send/receive is the model
- if processes P and Q want to communicate, they need to:
    - establish a connection
    - send message
    - receive message
- implementation:
    - how are links established? (pipes?)
    - how do we link multiple processes?
    - how many links between every pair of communicating processes?
    - what's the link capacity?
    - what's the size of a message?
    - is it unidirection or bi-directional?

### Direct Communication
- processes name each other explicitly
    - `send(pid=1, message)`

### Indirect Communication
- similar to mailbox system
- each process puts and pulls from a "mailbox" (a port)
- operations:
    - create a port
    - send and recieve messages through a mailbox
    - destroy mailbox
- `send(port=1, messsage)`

### Synchronization
- message passing can be blocking or non-blocking
- blocking: is considered synchronous
    - blocking send: the sended blocks until the message is received
    - blocking receive: receiver is blocked until message is available
- non-blocking: is considered asynch
    - non-blocking send: sends message and continues
    - non-blocking receive: receives a valid message or a null message
- if both send and receive are blocking, we have a rendezvous

## Communication
-- 1:04:36 -- 