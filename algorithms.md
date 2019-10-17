Algorithms
=====
Class notes from Computer Science 3020, Algorithms and Data Structures at the University of Wyoming. I took this class, and these notes, during the fall Semester of 2019.

Code and assignments associated with this class is available [here](https://github.com/andey-robins/school/tree/master/cosc3020/).

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
