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
-- stopped at 29:34 --