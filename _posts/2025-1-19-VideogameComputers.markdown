---
layout: post
title: "Computers Running Video Games Running... Computers?"
date: 2025-01-18 00:00:00
categories: Math Computer_Science Gaming
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

With the fires nearing UCLA last week, I evacuated back home, dreading online classes but content with the idea that now I hove slightly more free time to binge watch Youtube gaming channels. However, since I kept on watching videos by channels by Linus Tech Tips and other technical channels, the almightly Youtube algo threw a curveball straight into my feed and now I got videos of people building full computers from Minecraft redstone. With the image of running Minecraft on a redstone computer ***while*** playing Minecraft firmly ingrained in my head, I wanted to make a post showing off the technical prowness of gamers, displaying the variety of games that you can build a full (but laggy) computer in and a little description of Turing machine and their importance in all of this. 

## Minecraft (obviously)

Minecraft stands out as the quintessential sandbox game for in-game computer creation. Players have built impressive computing systems using redstone, a game element that functions similarly to electrical circuits. These creations range from fully functional 8-bit computers capable of running basic programs to working graphing calculators and even devices that can play simple games like Tetris or Snake. These redstone computers often use thousands of components and can take months to design and build, showcasing the incredible creativity and problem-solving skills of the Minecraft community.

Redstone works a lot like real life signals, having a high and low version of the signal, and there are machines that can read the signal, like lamps (which act like pixels of a display). Using other redstone components. one can build almost anything, from logic gates like below, to transistors.

<img alt="Redstone diagram" src='https://raw.githubusercontent.com/qerty2006/qerty2006.github.io/refs/heads/main/_site/assets/images/g05ar4oaspt61.webp'/>


Redstone also has its own unique mechanic that we can't utilize as easily in real life; signal strength. Unlike real life, signal strength in Minecraft is discrete, and can be read and produced effectivly by  redstone components like comparators. This means with the right circuitry, people have designed machines using this psuedo-analog signal system to made [MIDI inspired music machines] in Minecraft.


<img alt="Redstone signal strength" src='https://raw.githubusercontent.com/qerty2006/qerty2006.github.io/refs/heads/main/_site/assets/images/signal_strength_line.png'/>

If you want to learn more about redstone computing, I cannot recommend anyone more than [Mattbatwings] on Youtube. From [QR code generators] to [basic logic gate explanations], this channel not only showed me how to break servers with computationally complex operations but also gave me the building blocks to understand how regular computer chips work. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/osFa7nwHHz4?si=SDxvz2X0Ds1xsVR9" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

## Terraria (aka 2D Minecraft)

I joke about Terraria being just a 2-dimensional version of Minecraft, but it's own game with its own unique ways of sending signals: wires, with different color sending different signals that don't overlap. It even has ways to make [transistors], which are memory preserving circuits essential for real life computers.

<img alt="Redstone signal strength" src='https://raw.githubusercontent.com/qerty2006/qerty2006.github.io/refs/heads/main/_site/assets/images/uoatulrux2m91.webp'/>




A good channel for learning about Terraria circuit making is [From Scratch]'s video on [building a computer in Terraria]. I don't play this game nearly as much as i play Minecraft, so I can't explain as well the amazingness of this process.

<iframe width="560" height="315" src="https://www.youtube.com/embed/zXPiqk0-zDY?si=75Nk72XuoBFZjxGi" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>




## Why did I mention Turing machines before?

At the forefront of all this, the incredibly simple way to answer if you can make a computer in a game, video or otherwise, is one question: Is it Turing Complete?

### What's a Turing Complete System?

Imagine a person with a list of numbers written on a paper of arbitrary length. They can do only 3 things with it:

1. Read the symbol at the current position
2. Write a symbol at the current position
3. Move left or right one position

This simple model, known as a Turing machine, is capable of performing any computation that a modern computer can do. A system is considered Turing complete if it can simulate this Turing machine.


## Magic The Gathering (all hail card games)

With this new idea of what games can make computers within them, we can jump out of a computer, and into games of carboard and paper.

<iframe width="560" height="315" src="https://www.youtube.com/embed/pdmODVYPDLA?si=Zzzjbzg5bcfFmIG7" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

# Why should we care?

Though these may just seem like games for children (as a child I will be very disappointed if that is what you believe)

[Mattbatwings]:https://www.youtube.com/c/Mattbatwings
[QR code generators]: https://www.youtube.com/watch?v=ZizmvuZ3EFk
[basic logic gate explanations]: https://www.youtube.com/watch?v=osFa7nwHHz4&t=6s
[MIDI inspired music machines]: https://www.youtube.com/watch?v=V6X2BHpeLww
[transistors]: https://forums.terraria.org/index.php?threads/a-reference-guide-for-simple-logic-devices.81751/
[From Scratch]: https://www.youtube.com/@built-from-scratch
[building a computer in Terraria]: https://www.youtube.com/watch?v=zXPiqk0-zDY&t=204s