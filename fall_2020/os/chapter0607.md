Process Synchronization
=====
Message passing just uses the OS. Shared memory doesn't take much of it. Concurrent access to shared memory of a multi-threaded process can result in strange problems.

## Race Condition
When you have two or more processes using a shared resource where the output depends on their execution order.
It can be dificcult to debug because there's no ensured order.
The solution is to create atomic pieces of code (i.e. code that can only touch something if nobody else is using it)

### Preventing Race Conditions
1. ensure no two processes are ever in their shared critical section at the same time
2. Doesn't depend on speed of solution or execution
3. No process running outside its critical section may block another process
4. No process should have to wait forever

## Critical Section Problem
The critical section is where only one process can be executing that section of the code.
The problem then becomes how do we get multiple processes to take turns running their critical sections?

### Solutions
1. Disable interrupts before moving into a critical section
    - super terrible solution
2. Locks
    - use a new "lock" variable
    - when the lock is open, a process can go in and run, locking it behind itself and opening when its done
3. Turns
    - use a new "turn" variable
    - each process will wait when it isn't its turn, then runs when it is their turn
    - changes "turn" after being done
    - forces them to alternate
    - only works for two processes
4. Leave/Enter Region
    - uses turns and interest abstraction
    - a process waits when it's the other processes turn and they're interested in it
    - when they're done with the critical section, they turn off interest

Biggest problems come between when a variable is checked and when it is changed shortly after.

### TSL
- Test and set lock
- the atomic solution to that locking problem
- it copies and locks at the exact same time since it's a single assembly instruction
- then you just have to open the lock when you're done
- solves pretty much everything except for starvation

#### C++11 Mutex
```
mutex mylock;
mylock.lock(); // locking
// critical region code
mylock.unlock();
```

## Busy Loop Problem
- waiting in a busy loop, your priority crashes, and you're wasting your CPU time waiting

### Solution
- take your process off the CPU for a definite amount of time
- can use sleep() and wakeup()
    - a sleeping process can't wake itself
- can slowly get lots sleeping at once if interrupts happen in undesirable ways

## Deadlock
- easy to arrive at while using semaphores
- happens when two processes each close a semaphore and then wait on the other semaphore

## Semaphores
- Synchronization tool that doesn't require busy waiting
- Each semaphore contains a non-negative integer
    - used to count number of sleep/wakeups
- two operations on semaphores
    - wait() and signal()
- counting semaphore
    - integer value domain unrestricted
- binary semaphore
    - only 0 or 1
- C++ mutex can be used as a semaphore with value 1

### Problems
- biggest problem is incorrect usage of semiphores
- other primitives exist to try to help
    - monitors are the big one


### Code
```
Semaphore S; // initialized to 1
wait (S); // allows 1 process into the critical section
// critical section code
signal (S); 
```

## Monitors
- "an object oriented semiphore"
- a monitor guarantees only one process will be in the monitor at any given time
- uses wait and signal again