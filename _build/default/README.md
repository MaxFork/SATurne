![logo](planet.png)

# SATurne

**SATurne** is a simple functional style SAT solver written in [Coq](https://coq.inria.fr/). Its design is strongly inspired by [this article](https://web.archive.org/web/20201109101535/http://www.cse.chalmers.se/~algehed/blogpostsHTML/SAT.html). It is a tiny solver absolutely not designed for performances or scalability, but its minimalist functional structure makes him relatively easy to manipulate inside Coq. The opportunity was so beautiful so I decided to provide a verified implementation of this solver.

## Using this mini solver

**SATurne** takes as input formulas of the propositional logic in conjunctive normal form and outputs a list of possible assignments. If the problem is unsatisfiable, the output list is empty. Propositions are expressed as natural numbers.

The signature of the `resolve` function is :
```coq
resolve : list list literal -> list list literal
```

where a `literal` is either `Pos n` or `Neg n` and `n` is of type `nat`.
Lists of the output describe literals that should be true to solve the problem.
For instance, the output `[[Pos 1]; [Pos 2]]` means that a solution to the problem is to set the first variable to **true**, and all the others to **false** or to set the second variable to **true** and all the others to **false**.

## Loading the Coq module

The sources are located in the `src` folder. A `_CoqProject` and a makefile are provided. Simply type `make` in the `src` folder and SATurne is ready to be loaded in your favorite Coq editor.

## An example

Let's consider the following SAT problem :

```
A /\ B /\ C
C -> not B
```

We first convert it into CNF which 
gives 

```
{{A}, {B}, {C}, {not C, not B}}
```

Renaming `A`, `B`, and `C` as `1`, `2` and `3`, it gives an input for the solver :

```
Compute (resolve [[Pos 1]; [Pos 2]; [Pos 3]; [Neg 3; Neg 2]]).
```

Which naturally outputs `[]` since this problem is unsatisfiable.

## Project status

+ [x] core algorithm
+ [x] termination proof
+ [ ] correctness proof (this is really not trivial, any help is welcomed :) )




