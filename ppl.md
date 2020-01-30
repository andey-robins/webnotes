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
