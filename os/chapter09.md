Memory
=====
Programs need to be brought into memory, so how do we do that and get it to start? A program just ensures that it is between the base and limit for a user's processes. The question is how do we bind everything.

## Address Binding
The source code will have a symbolic address. The compiler will bind this to a relocatable address (i.e. 14 bytes from beginning). Then the linker will give it the ability to run at a specific location on the machine.

### Types of Binding Instruction
- compile time: only on embedded systems where you know everything that has to run ever
- load time: generates when the process is loaded (easiest)
- execution time: must be supported by the hardware

Logical vs physical addresses are the main distinction. We don't work with physical addresses often, since it needs to be changed when necessary, we use logical addresses. This is where the medium scheduler (memory management unit) comes in.

## MMU (Medium Scheduler)
- Used to map logical to physical addresses
- this can run dynamic allocation
    - the relocation register contains that mapping on systems that support it
- dynamic linking
    - linking pushed off to execution time
    - loads a code stub, then uses that to locate the appropriate library at runtime
    - might run into needing to worry about versioning of libraries and your code

## Swapping
- most machines pretend they have double their available memory
- memory is coppied out into swap space to create that functionality
- one modified version of swapping turns it on and off, which can increase performance in some cases
- the big problem with swapping is the time to perform a context switch

## Segmentation
- you can split up logical segments into individual pieces
- places chunks into segments
    - tracked in a segment table
        - requires all of the locations to now be tracked across segments and not just processes
        - relocation is dynamic since we can move it and just change the segmentation table
    - validity bits/priveleges are tracked by the segments
- a segment of code can be re-used so that two instances of something only need to load once

## Paging
- fixed for first fit/next fit/etc.
- a page table then tracks the order of the program that gets dropped into pages of memory