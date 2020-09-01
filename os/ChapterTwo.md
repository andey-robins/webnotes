Chapter Two
=====
In this chapter we begin to dive a bit more into the structures of operating systems themselves. This will encompass the specifics of the pieces that make up the operating system.

## Operating System Services
1. User Interface
    - the ways in which we're able to interact with the computer
2. Process Management
    - load programs into memory
    - run processes
    - end execution
    - handle errors or normal execution
3. I/O Operations
    - how a process interacts with the rest of the computer and its files
4. File system manipulation
    - opening, reading, and writing to files
    - getting listings of files and directories
5. Communications
    - communication between processes
    - communication between processes across a network
    - shared memory
6. Error detection
    - what happens when we detect an error?
    - how do we handle a process encountering an error?
7. Resource Allocation
    - separating resources out amongst multiple users and multiple jobs
    - resources: cpu cycles, main memory, file storage, i/o devices, etc.
8. Accounting
    - keeping track of which users use how much and what kind or resource
9. Protection and Security
    - control and use of resources, information and access

## Process Management
"Without doing process management, there really is no point to an operating system."

### Tasks of Process Management
- create
- load
- execute
- suspend
- resume
- terminate
- switch between processes
- communicate between processes
- synchronize processes
- allocate/de-allocate resources
- avoid deadlock

### System Calls
- system calls
    - how you call an operating system
- api
    - high level pieces used to call into the system calls
    - updates to operating system can change the system calls, but since the API doesn't change, it doesn't break everything

## Operating System Design
Design of an OS is not solvable, but some approaches have proven successful. Kernel size becomes a balancing act. If it's too small, then there's too little support at higher levels. If it's too big, then there isn't enough flexibility at the higher levels. Another problem is how do we actually generate an install for the Operating System. 

### Each begins with some user/system goals:
- easy to use, easy to learn, reliable, safe, fast
- easy to design, implement, maintain, flexible, reliable, error-free, efficient

### Two things:
- policy: what will be done
- mechanism: how it will be done

### General Implementation:
- Earliest OSes were entirely in assembly
- then Algol
- now C and/or C++
- nearly always a mix of languages now
    - scripting
    - systems languages in C
    - the higher level it gets, the easier it is to write but the slower you have to be

### DOS
The first OS with an impact. It needed to be very, very small. It fit onto a single boot disk (on a floppy disk). It wasn't well separated, and its interfaces and levels of functionality were tied together. The Application ran into the System program and the BIOS device. The System program ran into DOS device drivers and the BIOS device. Then DOS would feed into the BIOS. Sometimes applications didn't even need to interact with DOS, and they would just ignore it. It was fast and easy to implement, but difficult to debug, modify, or upgrade, and it had poor security, protection, and stability because the whole OS exists in memory at once.

### UNIX
UNIX OS was split into two parts: the systems programs and the kernel. The kernel encompasses everything below the system-call interface and above the physical hardware. It covers scheduling, memory management, and some file operations. 

### Layered Approach
The OS is devided into layers. Layer 0 is the hardware, all the way up to layer N which is the UI. Then each layer is only dependent on the parts above and below it.

### Microkernel Systems
The small kernel is a response to bloated kernels and the requirements of smaller embeded systems. These are so small that they're a lot easier to extend and port to different architectures, they're more reliable since there's far less code running on them, and they're more secure. One of the biggest downsides is that there is a huge performance hit since the kernel is passing messages back and forth between user systems (such as applications, the file system, or device drivers). The microkernel will only run interprocess communication, memory management, and CPU scheduling.

### Modules 
Most modern OSes use a module approach. It mirrors the idea of an object oriented approach to the OS. It loads specific modules into the kernel to run and can be extended with other modules. 

### Hybrid Systems
Modern systems are some hybrid between a monolithic system and a modular system. You can pull in modules for very specific tasks (for example floppy disk support).

## Operating System Debugging
Debugging Operating Systems is often a difficult and painstaking process. Most OSes will log a bunch of information when they crash. A core dump is failure of an application while a crash dump is failure of a kernel. Beyond debugging, we then go into performance work. We can work to improve that performance by removing bottlenecks.