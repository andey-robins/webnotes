Programs
=====
Notes and comments on the various programming assignments for this course.

Program 1
-----
This is essentially a refresher. It's a warm up and ensures you learn how to use git. It's a class that handles an array of queues (i.e. a QueueArray(4) is four queues in an array)

### Additional notes to clarify the assignment
- on `Enqueue(data, 3)` -> puts data into queue number 3
- Dequeue will always pull from queue 0 until that's empty and then work its way up through the queues
    - also returns the object (duh)
- on `Qsize(2)` -> returns the size of the second queue
- in `Qstat` ensure memory allocation is done correctly
    - make sure to use `new`

### Turning in Assignments
- follow formatting guidelines to the letter

- use the STL for stuff if you need it
- the `prog1-example.h` is an example header file
    - you can use this
- you may have commits in the midst of the ones presented

Program 2
-----
This is the first of the more complicated ones. Requires writing two separate programs: a *commander* and *process manager*. Model the example2 code provided in the fork, exec, pipe lecture. If written correctly, it should take about 5 minutes to run.

### Commander Process
- takes input from a command line
- passes them to the process manager
- do not open the file in the commander
    - easily pipe the file commands into the commander with `./cmdr < hw2_input`

### Process Manager
- will act as a scheduler
    - simulates the scheduling algorithm provided
- has to maintain a PCB table
- if you write C correctly, it will end by calling Q
- P will fork and execute all the code for the reporter
- you can use an array of 100 elements for the PCB table
- rid 0, 1, and 2 are all queue arrays
- formatting for output is provided in `addon.txt`