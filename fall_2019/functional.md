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

Exam 1 Postmortem
-----
1. a) `pipe:: (a -> b) -> (b -> c) -> (a -> c)`

    `pipe f g = g.f`

    very similar to compose, but `(.):: (b -> c) -> (a -> b) -> (a -> c)` and so f needs to come first (i.e. `g (f x)` or `g.f`)

2. iii) Write a tail-recursive version of int2Nat function

    Driver/Seed: `int2Nat k = i2n k Z`
    Base: `i2n 0 n = n`
    Recursive: `i2n k n = i2n (k - 1) (S n)`

    I was missing the driver so that there was no clear `Z` within my code which is what gives a valid `Nat` type

4. b) Write implementations of *all* and *some* using *foldr* or *foldl*.

    `all p = foldr (\x ans -> p x && ans) True`
    `all p = foldl (\ans x -> ans && p x) True`

    `some p = foldr (\x ans -> p x || ans) False`
    `some p = foldl (\ans x -> p)`

    folds capture within one pattern of recursion an entire tree of recursion with just one line
        `(...((x 'op' f) 'op' f) ... 'op' f)`
    you're kind of collapsing the list into one result

5. a) What is the type of function `(uncurry . curry)`?

    `(.)::(b -> c) -> (a -> b) -> (a -> c)`
    `(uncurry . curry):: ((a,b) -> c) -> ((a,b) -> c)`

    you got the type of `(.)` messed up dumb ass :p next time slow down and actually check for that stuff

Building a Calculator
-----
`module calculator where

data Exp = C Int | V String | Plus Exp Exp | Fun (Int -> Int)    deriving Show`

so C is a constructor that takes in an Int and returns an `Exp` expression.

`instance Eq Exp where`
    `(C 0) == (C 0) = True`
    `(C 1) == (C 0) = True`
    `(C 2) == (C k) = k >= 2`
    `(C k) == (C 2) = k >= 2`
    `V s1 == V s2 = s1 == s2`
    `_ == _ = False`

this is a crow-counter where you can only count up to 2. everything [0,2] can be accurately compared, but everything above that is simply treated the same
it defines the equal property `==` for our new data object

`instance Show Exp where`
    `show (C k) = show k`
    `show (V x) = show x`
    `show (Plus e1 e2) = "Plus " ++ (show e1) ++ (show e2)``
    `show (Fun f) = "Fun ... of something."`

this redefines the show function to show our `Exp` data type

Parsing
-----
Note: Functional Pearls: Monad Parsing in Haskell

What is the type of a parser?
String -> Tree
String -> (Tree, String) : this makes sure you parse the first part and don't discard the end part

Compiling
-----
`ghc -o cp cp.hs` will compile `cp.hs` into an executable called `cp`

`main = do`
`       (f1:f2:_) <- getArgs`
`       cp f1 f2`
`cp f1 f2 = {...}`

above is the boilerplate to get arguments and pass them to the function that does the work.

`getArgs::IO [String]`

Formulas
-----
formulas = ┴ | *x* | f_1 => f_2 | f_1 && f_2
┴ is false
x = {p, q, r, p_1, q_1, ... }
f_1, f_2 are formulas

in the types language, we could write implies as -> and && as a cross product

programming language terms = x | t_1 t_2 | lambda x t_1 | (t_1, t_2) | fst t_1 | snd t_1 | any x
x is vars = {x, y, z ...}
t_1, t_2 are terms and they represent apply t_1 to t_2

from there we can make sequents
([(String, Formula), [Formula]])

Basically, we constructed a program that takes a proof and then returns the program embedded in the proof

Final Review
-----
* No induction on lists stuff.
* folds and maps on trees
    * writing basic functions on trees
    * building a tree from lists
* a question where you have to write a small interpreter
    - `data Bool = V String | Not Bool | Bool 'AND' Bool | False | Bool 'OR' Bool | Bool 'WHERE' String Bool`
    - `eval::(String -> Int) -> Bool -> Int`
    - `eval a (V x) = a x`
    - `eval a (Not b) = (eval a b) + 1 mod 2`
    - `eval a (b1 'AND' b2) = (eval a b1) * (eval a b2)`
    - `eval a (False) = 0`
    - `eval a (b1 'OR' b2) =  (eval a b1) + (eval a b2)`
    - `update::(a,b) -> (a -> b) -> (a -> b)`
    - `eval a (b1 'WHERE' x b2) = eval (update(x, eval a b2) a) b1`
    - `|= eval a' b1 where a' = update(x, eval a b2)`
* "definitely some simple questions on parsers"
    * you will have some small example parser to remember how to put them together
    * you will also have access to the super basic parsers
    * the example parses the grammar defined in the left recursion part of this review, it just doesn't have the bool' part
    - `whereP b = do symbol "where"; x <- identifier; symbol "="; b1 <- boolP; return (Where b x b1)`
* small eliminate direct left recursion
    * algorithm will be given
* left recursion
    - `Bool = Var | "~" Bool | Bool "&" Bool | "True" | Bool "where" Var "=" Bool`
    * these are b1 | b2 | a1 | b3 | a2 where a is alpha and b is beta
    - `Bool  -> Var Bool' | Not Bool Bool' | True Bool'`
    - `Bool' -> AND Bool Bool' | WHERE Var = Bool Bool' | Epsilon`
    * More generally data is all (b data') where b are the betas
    * data' is (a data') | Epsilon where a is the alphas
* writing instances of the `Eq` typeclass
    * equality will be specified, and we just need to implement it
* nothing on `IO()`
