Scheduling
=====
The scheduler is traditionally *the* reason for an operating system to exist.

## Schedulers
- short term:
    - selects a process from ready queue
    - must be very fast
    - must be very efficient

### Concept of a Process
- CPU-I/O burst cycle
    - when a process starts up, it usually requires I/O
    - then alternates between CPU bursts and I/O bursts
- so, how do we decide what ready process to put onto the CPU next?

## Goals:
1. fairness or waiting time
    - amount of time spent waiting in the ready queue
    - no process will wait "too" long
2. CPU utilization
    - keep it busy most of the time
    - hopefully 40-90% of the time
    - doesn't include the scheduler in that timing
3. Response time (lag)
4. Turnaround time
    - time from submission to completion
5. Throughput
    - \# of processes that complete their execution per time unit

Since it's not really possible to do them all, the scheduler will optimize for a few of these options

### The Scheduler's actions
1. process switches from running to waiting
2. process switches from running to ready
3. process switches from waiting to ready
4. process terminates
Scheduling is under 1 and 4 is nonpreemptive
All other scheduling is preemptive

## Dispatcher
- gives control of the CPU to the process selected by the scheduler
- switches context
- switches to user mode
- jumping to the proper restart location

## Types of Scheduling
### Non-preemptive scheduling
- a running process is only suspended when it blocks or terminates
- pros:
    - decreases turnaround time
    - high CPU utilization
    - no special hardware required (i.e. a timer)
- cons: 
    - poor response time
    - poor fairness
    - limited choice of scheduling algorithms

### Preemptive scheduling
- a running process can be taken off the CPU for any reason
- pros:
    - no limitation on choice of algorithm
    - increased fairness
    - increased response time
- cons:
    - additional overhead (i.e. context switching)
    - decreased CPU utilization
    - longer turnaround time

### FCFS scheduling (non-preemptive)
- first come first served
- cpu goes to the process that requested it first
- pros:
    - simmple to understand and implement
    - fast selection for scheduling
- cons: 
    - average waiting time is long and varied
    - not suitable for time-sharing

### Shortest-Job-First (SJF) scheduling
- shortest job next: either preemptive or non-preemptive
- associate the length of a process for its next CPU burst
- pros:
    - minimum average waiting time
- cons: 
    - difficult to estimate CPU burst time
    - starvation (indefinite blocking) since every other job is shorter than yours

#### Determining Length of Next CPU Burst
- can only provide an estimate of the length which is the problem

### Round Robin Scheduling
- preemptive
- most widely used
- very simple to write
- very very fair
- each process is given a "quantum" or "time slice"
    - if the process is still running at the end of the quantum, it gets pulled off the CPU and put back in the queue
    - if your program blocks or terminates, the quantum is ended
- higher average turnaround than SJF, but better response time

#### Questions about RR
- how long should the quantum be?
    - too small, spend too much time context switching
    - too big, poor response time
    - typilly between 10 and 100 ms
    - the quantum time could change quantum size itself, but that adds too much complexity

### Priority Scheduling
- not all processes are equally important, so each one gets some sort of priority
- if multiple have the same priority, round robin among those
- a priority integer is associated w/ each process
- problem - los priority processes may never execute
- array of priority queues
    0. P -> Q -> R
    1. O -> S
    2. 
    3. A
    4. C
    - the problem arrises when P, Q, and R will require days while A only needs 30 seconds
- to solve the problem, implement aging
    - the longer a process has sit in the queue, the higher its priority will be

#### Multiple Queues with Dynamic Priority
- processes are once again divided into 2 classes
    - CPU bound
    - I/O bound

- if you know the process is:
    - I/O bound then it will use the processor for a shorter time
    - therefore they get higher priority

- should I/O and CPU quantums be the same?
    - vary quantum w/ dynamic priority (program 2 in a nutshell)
    - higher priority = lower quantum and lower priority = higher quantum

- how do we know I/O vs CPU bound?
    - figure it dynamically
    - any process coming in has priority 0
    - if a running process uses its quantum, then lower its priority by 1
    - if the process blocks, raise the priority by 1

### Multi-Processor Scheduling
- very complex
- if the processor is heterogenoous, then it's very difficult to determine what goes where and when
- if it's homogenous, then its a question of load balancing
    - symmetric vs asymmetric
    - symmetric:
        - each processor self-schedules
        - need to synch the schedulers
    - asymmetric:
        - one CPU becomes the master and is in charge of giving processes to other processors

- affinity:
    - processor wanting to stay on the CPU it's already on since it has the quicker access to that memory

### Multicore Processors
- multiple processors on the same physical chip
- removes the memory problems of multi-processors through mutlithreading