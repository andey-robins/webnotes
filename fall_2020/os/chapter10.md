Virtual Memory
=====
All of the code doesn't need to be loaded at any given time for a program, so we can partially load a program. Virtual memory is a way to abstract the physical memory to a logical memory level.

## Algorithms
Frame allocation:
    - how many frames to give each process
    - which frames to replace
Page Replacement algorithm:
    - want lowest page-fault rate

### Random Selection
- not clearly a bad algorithm
- very fast
- may impact your process performance, but doesn't impact your OS

### Optimal Selection
- used for analysis only
- runs into the halting problem since it requires all knowledge

### First In First Out
- takes the page that's been in longest and kicks it out
- strange anomaly where more pages doesn't always mean less page faults

### Optimal
- replace page that will not be used for the longest period of time

### Least Recently Used
- replace the page used the longest ago

### Counting Algorithms
- least frequently used
    - replace page with smallest count
- most frequently used
    - replace page with highest count

### Page Buffering
- keep a pool of free frames
- read in a new page and then kick out another page