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
This is the first of the more complicated ones. Requires writing two separate programs: a *commander* and *process manager*. We'll come back to it after the fork, exec, pipe lecture.