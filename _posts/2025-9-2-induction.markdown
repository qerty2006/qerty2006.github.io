---
layout: post
title: "Beginner's Guide to Mathematical Induction"
date: 2025-02-02 00:00:00
categories: Math Games Logic 
author: 'Nishanth Tharakan'
---

<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$$','$$'], ["\$$","\$$"] ],
      processEscapes: true
    }
  });
</script>

<script type="text/javascript" charset="utf-8" 
src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML,
https://vincenttam.github.io/javascripts/MathJaxLocal.js"></script>

As a UCLA student, I had my first midterms of the winter quarter last week, taking Differential Equations, Intro to C++, and Introduction to Discrete Structures, the last of which has become one of my favorite classes. Though I'm not a pure math major (applied all the way!), I love learning about new ways to do mathematical proofs, and I wanted to share more about my favorite method of proof: induction.

## Dominos of Logic

Induction works like a set of dominoes, lined up, ready for someone to come and knock it over.

Typically when a domino is hit by another domino, it falls over, usually hitting another domino, so we can write a little math statement like:

$$ \text{Domino behind has fallen} \implies \text{Domino has fallen} $$

This is a quick way to say "The fact that the previous domino has fallen implies it knocks down the next Domino and that one has fallen now." 
 
Now all we need to complete the dominoes by knocking one down, cascading through the rest and knocking all further ones down. Then:

$$ \text{Domino 1 has fallen} 
\rightarrow \text{Domino 2 has fallen} \rightarrow  \text{Domino 3 has fallen}  ...  $$

## Example: Divisibility

A common example problem used when teaching induction is proving $$4^n - 1$$ is divisible by 3 for all n. Let's do a formal proof:

$$ \text{WTS (want to show) } 4^n -1 \equiv 0 \quad(\text{mod 3}) \text{ for all } n \in \mathbb{Z}^+$$

### Base case (show the first domino has fallen down):

Substituting $n = 1$ into the expression gives us:

$$4^1 - 1 = 4 - 1 = 3$$

Since 3 is divisible by 3, the statement is true for $n = 1$.

### Inductive Hypothesis
Assume that the statement is true for some positive integer $k$, i.e., assume that:

$$ 4^k -1 \equiv 0 \quad(\text{mod 3}) $$

This means $4^k - 1$ is divisible by 3.

### Inductive Step (show that a previous domino can knock down the next domino)
We need to show that if the statement is true for $n = k$, it is also true for $n = k + 1$. That is, we need to prove:

$4^{k+} - 1 \equiv 0 \quad(\text{mod 3}) \rightarrow 4^{k+1} - 1 \equiv 0 \quad(\text{mod 3})$

Starting with $4^{k+1} - 1$, we can rewrite it as:

$$4^{k+1} - 1 = 4 \cdot 4^k - 1 = 4 \cdot 4^k - 4 + 3 = 4(4^k - 1) + 3$$

Since $4^k - 1$ is divisible by 3 (by our inductive hypothesis), $4(4^k - 1)$ is also divisible by 3. Adding 3 to a number divisible by 3 results in another number divisible by 3. Therefore, $4^{k+1} - 1$ is divisible by 3.

### Last Statement
By mathematical induction, we have shown that $4^n - 1$ is divisible by 3 for all positive integers $n$.

This is effectively the main way to solve a lot of formula based induction problems; rewrite $n_{i+1}$ in terms of $n_{i}$ , show the statement is true for $n_1$ (or some starting point, not necessarily 1), then show it's true for $n_{i+1}$ when it's true for $n_{i}$, and the game is over. 

But there is a visual problem where we can use this method: 

## Example: Degenerate Square Tiling:
<img src="https://nstarr.people.amherst.edu/trom/v-21.gif" alt="nstarr.people.amherst.edu"/>

This problem is really fun: show that if you are given a square with size $2^n \times 2^n$ and remove 1 tile, no matter what tile you remove, you can use trominos (3 piece tiles in an L shape) to tile the rest of the board.

**Base Case**: For $n = 1$, the degenerate square is a $2 \times 2$ square with one tile removed. This can be tiled with one angular tromino if the removed tile is in a corner, which it will always be.

**Inductive Hypothesis**: Assume that a degenerate square of size $2^k$ can be tiled with angular trominos.
    
**Inductive Step**: Divide a degenerate square of size $2^{k+1}$ into four quadrants. Only one quadrant (of size $2^n \times 2^n$) will have the degenerate tile, so by the Inductive hypothesis we can tile that quadrant.

Now we have 3 other non degenerate quadrants (in an L shape) that we need to tile. We can "make" them degenerate by taking the 3 corners they have closest to each other (this will be in an L shape) and placing a tromino there. This makes the rest of the quadrants into degenerate $2^n \times 2^n$ squares since they all have exactly 1 square missing (their corner) and thus can be tiled by the Inductive Hypothesis.

**Conclusion**: By the Principle of Induction, since $P_1$ (tile a $2^1 \times 2^1$) is true, and we showed that we can tile a $2^{n+1} \times 2^{n+1}$ given we can tile a $2^n \times 2^n$ square, our original problem is solved.                  

## Why does this matter?

I feel that induction is one of the most intuitive ways to prove something, and it makes sense why it’s one of the first methods one learns in an introductory proof class. However this method is used for much more for divisibility and tilings; the [Tower of Hanoi](https://en.wikipedia.org/wiki/Tower_of_Hanoi), a famous game where you stack disks on top of each other, trying to move all the disks to a new tower while keeping them in the same relative order, has a proof for the fastest possible game being $$2^n - 1$$ turns for a game with $n$ disks. Induction is also a good way to check an initial hypothesis before writing a formal proof, many times by disproving it in the inductive step and moving on. 

Regardless, learning induction helps build foundational understanding and confidence in mathematical reasoning, which is essential for tackling more advanced and complex problems in mathematics and related fields. Whether you're an applied math student like yourself or a pure mathematician, mastering induction is a valuable skill that will serve you well in your mathematical journey.

