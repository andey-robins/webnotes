Virtual Machines
=====
At its root, we're going to fake the underlying pieces of a system. VMs came from IBM in the 70s when they had to solve the problem of keeping code running for 30 years as proised while still being able to change the underlying hardware of their systems.

## Components
- Host -> the underlying hardware of the system
- VMM -> virtual machine manager/hypervisor creates and runs a system by providing an API that is identical to the host
- Guest -> the process given a virtual copy of the host, which is usually an OS

## Types
- Type 0: hardware based, i.e. the VMM is your firmware
- Type 1: functionally the "base" operating system on a device; or, things that have the VMM built into the OS, i.e. WinServ
- Type 2: Virtualbox, etc.
- Paravirtualization: A VMM that runs in tandem with the OS
- Programming Environment: i.e. JVM
- Emulators: simulate different hardware through software
- Sandboxing
