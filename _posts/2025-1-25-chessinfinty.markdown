---
layout: post
title: "Forever and Ever: Infinite Chess And How to Visually Represent Infinity"
date: 2025-01-26 00:00:00
categories: Math Games Infinity
author: 'Nishanth Tharakan'
---

<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>


<script type="text/javascript" charset="utf-8" 
src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML,
https://vincenttam.github.io/javascripts/MathJaxLocal.js"></script>


Many people enjoy chess, and with its popularity, chess has a major online presence, and dozens of famous variations of the game, like [Bughouse] and [Losing Chess]. While researching for my last post on the Magic the Gathering Turing Machine, I found both a [Youtube video] and a [paper] (by C.D.A. Evans and Joel David Hamkins) describe a unique variant of chess, one with a large board, infinite in size in every direction. Today I'll explain checkmate, ordinals, and how a set of pieces can represent infinity.

## Checkmate in Infinite chess

For those who don't play chess, checkmate is the end result of the game, where a king is unable to move to a situation where they will not get captured the next turn. 

<img alt="Example of checkmate" src='https://raw.githubusercontent.com/qerty2006/qerty2006.github.io/refs/heads/main/_site/assets/images/checkmateex.webp'/>


The pawn attacks the king, and the edges of the board along with the bishop prevents the king from moving. But in infinite chess, the board cannot restrict movement; when a piece has an unobstructed path, they can pick a direction and a number n, and then move that many spaces in that direction. This means an unblocked rook could move 2, 50, or 1,005,688,288,434 spaces to the right, and still be on the board.

An example of Checkmate-in-N is the diagram below, taken from the paper: 
<img alt="Example of checkmate" src='https://raw.githubusercontent.com/qerty2006/qerty2006.github.io/refs/heads/main/_site/assets/images/mateinn.png'/>

The black king can only move backwards to avoid mate, and the queen and rook will follow, eventually mating when the kings are almost touching. In this case, if each side plays optimally , the game will always end within N moves, where N is the distance between the kings.

## Time for Mate in ω

Mate in ω can be thought of "Schrödinger's" mate; you know it will result in checkmate, but given a position, you could have a mate-in-1, a mate-in-2... as high as you want based on the next move played:

<img alt="Example of checkmate" src='https://raw.githubusercontent.com/qerty2006/qerty2006.github.io/refs/heads/main/_site/assets/images/mateinω.png'/>






[transfinite chess]: https://arxiv.org/pdf/1302.4377
[Bughouse]: https://en.wikipedia.org/wiki/Bughouse_chess
[Losing Chess]: https://en.wikipedia.org/wiki/Losing_chess
[Youtube video]:https://www.youtube.com/watch?v=b-Bb_TyhC1A
[paper]: https://arxiv.org/pdf/1302.4377