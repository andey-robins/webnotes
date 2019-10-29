Functional Programming
=====

Class notes from Computer Science 3015, Functional Programming at the University of Wyoming. I took this class, and these notes, during the fall Semester of 2019.

Code and assignments associated with this class are available [here](https://github.com/andey-robins/school/tree/master/cosc3015/homework).

An excellent book to check out is Learn You a Haskell for Great Good: A Beginners Guide.

I'm going to be totally real here too, I don't actually know what this class is about and we're basically half way through the semester

Curry and Uncurry
-----
||curry|uncurry|
|---|---|---|
|definition::|((a,b) -> c) -> (a -> (b -> c))|(a -> (b -> c)) -> ((a,b) -> c)|
|function call|f (x, y)|f x y|

Proofs
-----
Handwritten proofs are contained in the Onenote notebooks used for this class. They are simply demonstrations of inductive proofs written out by me, and so they may not be much help. I haven't included them at this time because they seem to not be anything other than properties about the functions in haskell.

Homework Review
-----
definitions for the exam will be provided in a manner similar to the homework
proofs that two functions are equal should also include a proof that their types are the same

to prove two functions are equal, show that forall arguments, they are the same

no need to include "justifications" for the actions you take on the table
the empty list is an element of all types -> you can use it as a catch all for a result of type list
`f :: [a] -> (a -> b) -> [b]` -> `f _ _ = []`
`f :: Maybe a = Just a | Nothing` -> `f _ _ = Nothing` -> `f [] g = Nothing && f (x:xs) g = Just (g x)`

a tail recursive function is one where an accumulator goes down the call stack with it and then is returned with the result as soon as it hits the bottom
`data Tree a = Leaf | Node a (Tree a) (Tree a)`
`Leaf:: Tree a`
`Node:: a -> (Tree a) -> (Tree a) -> Tree a`

Warning: Caldwell roasts Gamboa and everyone laughs. World peace is achieved. Obama is there. It is wonderful.

on the length proof from hw6, add one more step to show that `|x:xs| + |ys|` = `1 + |xs| + |ys|`

`foldl` and `foldr` behave the same when the operator is associative

Exam 1 Contents and Review
-----
 * curry and uncurry
 * question similar to Theorem 1.3's proof on HW 2
 * left or right identity
 * type inferencing
 * write a function from a type definition
 * tail recursive version of length
 * type of cons and append <- this will explicitly be on the test
 * write constructors and give their types for a data structure
 * write a tail recursive function on the above data structure
 * list induction and proofs
 * foldl and foldr

Hint: `f :: a -> b -> ((a,b) -> c) -> c` = `f x y g = g (x,y)`

- 5 questions
- 75 minutes
- regular meeting place
- minor syntax errors will only result in minor deductions

Building a Calculator
-----
`module calculator where

data Exp = C Int | V String | Plus Exp Exp | Fun (Int -> Int)    deriving Show`

so C is a constructor that takes in an Int and returns an `Exp` expression.

`instance Eq Exp where
    (C 0) == (C 0) = True
    (C 1) == (C 0) = True
    (C 2) == (C k) = k >= 2
    (C k) == (C 2) = k >= 2
    V s1 == V s2 = s1 == s2
    _ == _ = False`

this is a crow-counter where you can only count up to 2. everything [0,2] can be accurately compared, but everything above that is simply treated the same
it defines the equal property `==` for our new data object

`instance Show Exp where
    show (C k) = show k
    show (V x) = show x
    show (Plus e1 e2) = "Plus " ++ (show e1) ++ (show e2)
    show (Fun f) = "Fun ... of something."`

this redefines the show function to show our `Exp` data type
