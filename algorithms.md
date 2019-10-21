Algorithms
=====
Class notes from Computer Science 3020, Algorithms and Data Structures at the University of Wyoming. I took this class, and these notes, during the fall Semester of 2019.

Code and assignments associated with this class is available [here](https://github.com/andey-robins/school/tree/master/cosc3020/).

Time Complexity Information
-----
the master's theorems are a way to simply calculate the time complexity of code without tracing a recurrence relation

|Operation|Time Complexity|
|---|---|
|single operation|constant|
|consecutive operations|sum operation time|
|conditionals|condition time + max branch time|
|loops|sum of loop-body times|
|function call|time for function|

###Asymptotic Behavior
- find runtime as a function of *n*
- can ignore constants in final complexity
- is really meaningful when *n* is large

Sorting
-----
y'know what sorting is. It's basically just trying to put things in order.

###Loop Invariants
a loop invariant is something that can be said about the loop at any given iteration
for instance, the loop invariant for insertion sort is: after each iteration of the loop, elements [0..i-1] are sorted
using a loop invariant, you can eventually show that an algorithm is correct

####Finding Invariants
First ask, "What would be true about this data after every loop?"
Functions similarly to a proof by induction where the loop invariant is the induction hypothesis

###Insertion Sort
Worst Case : *θ(n^2)*
Best Case : *θ(n)*

###Heap Sort
1. heapify input
2. remove minimum value
3. repeat *n* times

Worst Case : *θ(n log n)*
Best Case : *θ(n log n)*

###Merge Sort
divide and conquer algorithm

1. if an array has 0 or 1 elements, it's sorted
2. split the array into two halves
3. sort each half recursively
4. merge the two halves into a single, sorted partition

Searching
-----
searching deals with the ways we move through graphs

###Search Types
- depth first search (DFS)
    - go as far down a path as possible
    - slowly backtrack to search through every possible solution
    - usually done with recursion
- breadth first search (BFS)
    - expand from the center outwards in "steps"
    - search wide instead of deep
    - makes use of a queue
- best first search
    - breadth first search with a priority queue
    - priority is assigned with some sort of heuristic function
    - dijkstra's algorithm and A* are some examples of best first search algorithms

Assignment 1 Review
-----

My work for this assignment can be found [here](https://github.com/andey-robins/school/tree/master/cosc3020/hw/01)

1.  proofs need to be self contained
    the intuition for writing proofs is that they should be code. It needs to know every little detail
    big O is a set of functions
    $$f(x) \in O(g(x)) \implies \exists c,n_0 : f(n) \leq c \cdot g(n) \all n \geq n_0$$
    remember all parts of the definition (i.e. the \\(n \geq n_0$$ part\\))
    transform the logarithms using log rules
    after they're in the same terms of logarithms, substitute one into the other so that you have the old function in terms of the new logarithms
    then, after you show one implies the other, then do it the other way; that's how you get the full proof

2.  weird multiplicities can be simplified if you can reason that they will converge
    you can also do it by solving for geometric series
    be careful with the difference between regular multiplication and things being raised to a factor
    \((T(n/3)\\) will always hit \\(T(1)\\) due to the construction of our piecewise. if it doesn't, you picked the wrong \\(i\\)

3.  take a look at other people's formatting, because i'm not happy with the way it was formatted
    good job :)

4.  strong implementation :)
    for the time complexity discussion, it would have been good enough to simply look at what changed from `mergeSort` to `inplaceMergeSort`

5.  be very careful when using mixed notation (i.e. decimal probabilities and percentage probabilities)
    include full calculations for fractions to try to avoid errors
    the approach of representing all possible locations picked from and then checking which representations resulted in good picks, then yes
