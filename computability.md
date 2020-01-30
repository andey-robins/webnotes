Computability and Complexity
=====
Class notes from Computer Science 4200, Computability and Complexity at the University of Wyoming. I took this class, and these notes, during the spring semester of 2020.

<!-- Code and assignments associated with this class is available [here](https://github.com/andey-robins/school/tree/master/cosc3020/). -->

Introduction
-----
Simply, this class is "which problems can be solved on a computer?"

There are 4 different models of algorithms
- Finite-State automata
    - algorithms with limited memory
- Pushdown automata
    - algorithms that work with a stack architecture
- Turing machines
    - any algorithm that can be on a turing machine
- Polynomial time algorithms
    - efficiently solvable algorithms

Finite State Automata
-----
These are algorithms that operate with a limited amount of memory.

###Finite Automata Key
- circles are states
- q_0 is often the initial state (an unlabeled arrow marks the entry point)
- a state with two circles is an "accepting state"
    - sometimes also denoted by a circle within a square
- labeled arrows are transitions
- after reading in a string to the machine, it reads each bit in succession, moving to the state indicated by the input. if the machine ends in an accepting state, the machine accepts the string; otherwise the machine rejects the string.
    - *M* denotes the machine
    - *w* denotes the string
    - *{0, 1}\** denotes the set of all possible binary strings

####Definition of a (Deterministic) Finite Automaton (DFA)
A deterministic finite automaton is a 5-tuple M = (Q, Σ, 𝛅, q_0, F) where:
- Q is finite set of states
- Σ is an alphabet
- 𝛅 : Q x Σ -> Q is the transition function
- q_0 in Q is the initial state
- F is a subset of Q and is the set of accepting states

Beyond that mathematical definition, a number of further definitions for related sets and symbols follows.

- *𝛅(q, a) = r* -> means the DFA transitions from state *q* to state *r* when it reads symbol *a*
- Σ\* is all finite strings of symbols from the alphabet Σ
- a "language" is a subset of Σ\*
    - a language can also be called a "decision problem"
- 𝜀 is the empty string of length 0
- for any string *w* in Σ\*, *w_i* is the ith symbol of *w*

####Definitions of Acceptance in a DFA
Let M = (Q, Σ, 𝛅, q_0, F) be a DFA:
1. Let *w* be in Σ\*. We say that M accepts *w* if there is a sequence of states r_0, r_1, ... r_|w| in Q such that:
    - r_0 = q_0
    - 𝛅(r_i, w_i+1) = r_i+1 for all i: 0 ≤ i < |w|
    - r_w in F
2. The language accepted by M is L(M) = { w in Σ\* | M accepts w}

Effectively, a DFA accepts a word if, on that input, the DFA will conclude on an accepting state. The set of all words that fit within the language is then denotes at L(M)

Alternatively, you can define it inductively using an extension 𝛅\* : Q x Σ\* -> Q for all q in Q, 𝛅\*(q, 𝜀) = q and for all q in Q, w in Σ\* and a in Σ, 𝛅\*(q, wa) = 𝛅(𝛅*(q, w), a). In this statement, a is a character while w is a string. It's effectively extending the string indefinitely a la an inductive proof (woah). Defining 𝛅\* as an extension allows us to include an action where we do nothing on the empty string, which enables the base case of the inductive proof.

Let M = (Q, Σ, 𝛅, q_0, F) be a DFA. Let w in Σ\*. We say that M accepts w if 𝛅\*(q_0, w) in F. The language accepted by M is L(M) = { w in Σ\* | 𝛅\*(q_0, w) in F }.

####Regular Languages
A language is regular if it is the language for some DFA. B subset Σ\* is regular if B = L(M) for some DFA M. The DFA can distinguish if the language is regular if M accepts w.
