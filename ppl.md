Principles of Programming Languages
=====
Class notes from Computer Science 4780, Principles of Programming Languages at the University of Wyoming. I took this class, and these notes, during the spring semester of 2020.

<!-- Code and assignments associated with this class is available [here](https://github.com/andey-robins/school/tree/master/cosc3020/). -->

Introduction
-----
This course concerns itself with the mathematical meaning of the abstract syntax trees that are parsed by a compiler. They are a tree representation of a program.

"What is the meaning (semantics) of a program?" is our guiding question.

Taxonomy of Programming Languages
-----
In the top level, programming languages are broken up between imperative and declarative languages. Imperative languages are prescriptive while declarative ones are descriptive. In a prescriptive language, you do this; do this; do this; and then have a result. A descriptive language says what form the answer will take and then it results. HTML would be an example of a descriptive language. From declarative languages, you have functional and logical programs (PROLOG is the logical programming language); constraint programming languages also fall in this field, though they are an incredibly small number of languages. Constraint languages are similar to PROLOG without the requirement for descriptions to be logical in nature. As far as functional languages go, LISP was the first in 1959-ish, which was followed by Haskell, ML, Clean, and others. The first imperative language was FORTRAN created at approximately the same time. Effectively every other language, virtually all of the big ones, and most of the ways that you think fall into this category of languages.

Language Construction
-----
In the field of programming languages there is syntax, or the form of languages, and semantics, or the meaning of languages. In the realm of syntax, BNF, or Backus Naur Form, is the way that we describe the form of the language; alternatively, context free grammars can be used to describe the syntax. On the other side, in order to describe symantix we can use axiomatic semantics, denotational semantics, and operational symantics. One reductive way to think of semantics as if two programs produce the same outputs given the same inputs. They effectively do the same thing.

Context free grammars are languages where the meaning is not dependent on where clauses occur within the language. This is a part of compositional languages where the meaning of the whole is a function of the meaning of the parts. A language is a subset of Σ\* where Σ is an alphabet and Σ\* is a set of all words in that alphabet. We know how to write algorithms that recognize the elements of a context-free grammar language. Context sensitive languages are neither compositional nor do we know how to write algorithms to understand them.

Mathematical Fundamentals Review
-----
A brief review of the mathematic fundamentals for this class.

###Boolean Connectives
&& - and
|| - or
-> - implies
! - not
<=> - iff: p->q && q->p

|p|q|p && q|p or q|p -> q|!p|p< => q
|---|---|---|---|---|---|---|
|T|T|T|T|T|F|T|
|T|F|F|T|F|F|F|
|F|T|F|T|T|T|F|
|F|F|F|F|T|T|T|

###Quantifiers
upside down A - forall
backwards E - exists

forall X:T.F
exists X:T.F

X is a variable
T is a type or set
F is a formula

###BNF For Formulas
F := x | !p | p && q | p || q | p -> q | forall x.p | exists x.p | ... (other things that create arithmetic formulas)

x in var; var = {x, y, z, x1, y1, z1, x2, y2, z2, ... }
P, Q in F

forall x. exists y. y + y x
the above statement is true based upon what the domain of discourse is.

a way to conceptualize this is that: forall x:N. p(x) says that p(0) && p(1) && p(2) && ...
exists x:N. p(x) says that p(0) || p(1) || p(2) || ...

###Relations
Note: We write xRy to mean <x,y> in R

If R subset AxA, then:
  * R is reflexive iff forall x:A. <x,x> in R
  * R is symmetric iff forall x,y:A. xRy -> yRx
  * R is transitive iff forall x,y,z:A. (xRy && yRz) -> xRz

If you satisfy all three of these properties with a relation, then it's an equivalence relationship.

Abstract Syntax
-----
The following syntactic categories are defined.

###Syntactic Categories
 * n in Num - Numerals: "0" "1" "110" "90"
 * x in Var - Variables
 * a in Aexp - Arithmetic Expressions
 * b in Bexp - Boolean Expressions
 * S in Stm - Statements

###Formation Rules
Notably, the statement descriptions are missing expressions. The if statement wouldn't be able to do something such as `x = if x < 0 then 7 else x+1` as is done in haskell.

 * S ::= x := a | skip | S1;S2 | if b then S1 else S2 | while b do S
 * a ::= n | x | a1 + a2 | a1 * a2 | a1 - a2 | (a)
 * b ::= a1 = a2 | a1 < a2 | !b1 | b1 && b2 | (b1)

###Conventions
 * write a1 != a2 for !(a1 = a2)
 * S1; S2; S3 means S1; (S2; S3)
    * the book calls this left associative.
    * it's actually right associative
 * A transition system is a triple (Γ, ->, T)
    * Γ is a set of "configurations"
    * -> is a subset of Γ x Γ and is called the transition relation
    * T is a subset of Γ is the set of terminal configurations

###Big Step Semantics (AExp)
 - Γ = AExp U INT
 - -> subset AExp x INT
 - T = INT
