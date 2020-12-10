File Systems
=====
How do we create persistent memory?

A disk is divided into equal sized blocks, and the blocks are what we access/interact with.
The first block on the disk is the super block, and it contains information about partitioning.

## Virtual File System
- an object oriented way of doing a file system
- creates a top level api so that every file system command is the same