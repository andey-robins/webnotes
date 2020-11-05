File System Interface
-----
We want to have the concept of a file and we want to store it long term.

## File Attributes
- name
- identifier (unique tag)
- type
- location
- size
- protection
- time, date, user id

### Operations
- create
- read
- write
- reposition within file (see)
- delete
- truncate (delete from current position)

## Opening Files
- open (file handle) -> a pointer to memory for the ssystem called reference to the file
- close -> move contents from memory back to disk
- Open File Table
    - tracks the files that are open
- file pointer
    - pointer to last active location

## Directories
- some  collection of nodes containing information about files
- points to a file