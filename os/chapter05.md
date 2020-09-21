Threading
=====
Threads run within an application (process). It's the ability to do simple tasks in parallel. Since process creating is heavy, and thread creation is light, it's far easier to make a process do multiple things by threading instead of forking. It also leverages the fact that most kernels are multithreaded.

### Benefits
- resonsiveness
- pass through
- resource usage

### Limitations
- schedulers only see processes not threads
- if 1 thread blocks for I/O then the whole process gets taken off the CPU

## Multicore Programming
- multicore/multiprocessors put pressure on programmers to use as many cores as you paid for.
- what do we want to do?
    - divide activities
    - balance load
    - split up data
    - daata dependencies become challenges
    - testing and debugging is hard
- parallelism -> a system can perform multiple tasks at once
    - data parallelism: distributing subsets of data and doing the same operation on each
    - task parallelism: distributing threads across cores, each one performing unique actions
- concurrency -> supports more than one task making progress

## Multithreading Models
### Many-to-One
- many user level threads -> single kernel thread
- any one blocking stops all the threads

### One-to-One
- map your thread to a kernel thread
- more concurrency
- number of threads can be resitrected due to overhead

### Many-to-Many
- multiple user threads map to multiple kernel threads
- as a kernel thread becomes available it picks up a user thread
- allows threads to block on I/O since other threads will get picked up
- fewer kernel threads necessary
- while still being more parallel, not everything executes at will

### Two-level Model
- Allows a user thread to be bound to a kernel thread