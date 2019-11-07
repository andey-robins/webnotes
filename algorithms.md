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
searching deals with the ways we move through graphs and try to find specific elements

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

Network Flow
-----
graphs with edge capacities
designated source and target vertices
flow into a vertex must equal flow out of a vertex
e.g. roads, water networks, LAN cables
the question is at any given point, how much data can we push from source to target

###Ford-Fulkerson Algorithm
an algorithm to determine the network flow of the network:

- set flow to 0 for all edges
- construct another graph with "remaining capacity" (maximum at the beginning) for all edges
- while there is a path in the new graph
    - find the maximum flow for the path
    - add the flow to each edge on the path in the original graph
    - in the new graph
        - reduce the remaining capacities for each edge on the path
        - add a "return edge" (an edge moving in the opposite direction but connecting the same nodes) with the amount of flow that was pushed through this time
        - delete all edges with capacity 0

O(|E|*f*) where *f* is the maximum number of augmented paths in the graph

NP Completeness
-----
- *n* queens problem
    - place *n* queens on an *n x n* board such that none of them are attacking each other
    - O(n^2n) (if we allow multiple queens on each tile)
    - O(n^n) (consider rows instead of tiles)
    - O(n!) (one queen per row and consider permutations)

- "quality" of a decision only becomes apparent after making the choice
    - sometimes long after making the choice
- may need to make decisions to act intelligently
- difficulty comes from not knowing what choices to make

###Properties of NP Problems
- hard to solve; easy to check
- NP-hard: problem that is at least as hard as the hardest NP problem
- NP-complete: NP-hard and in the complexity class NP (i.e no harder)

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

Dynamic Programming and Memoization
-----
the idea behind dynamic programming is to take the algorithms we've been working with and make them more efficient by removing repeated work.

tail recursion fits into this area. a function is "tail recursive" if for any recursive call in the function, that call is the last thing the function needs to do before returning. you can always think about converting to a tail recursive solution if it would be easy, because then you get automatic compiler optimizations

###Fibonacci
instead of doing two branches down the tree, we want to "share" results/nodes.

there are two big ways to do it, bottom up dynamic programming (i.e. working up from the bottom of the call tree instead of working down from the top), or memoization where you save the values when you compute them and instead just check if the value already exists.

bottom up is calculating it in the same way a human would.

memoization is like a blend. it uses recursive calls, but it stores found values so they aren't computed twice. the big downside of this implementation is that there can be very large memory overheads.
