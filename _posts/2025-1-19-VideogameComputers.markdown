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


With the fires nearing UCLA last week, I evacuated back home, dreading online classes but slightly happy with the idea that now I have a little more free time to binge watch Youtube gaming channels. However, since I keep watching videos by channels by Linus Tech Tips and other technical channels, the almighty Youtube algo threw a curveball straight into my feed and now I get videos of people building full computers from Minecraft redstone and Factorio conveyor belts. With the image of running Minecraft on a redstone computer ***while*** playing Minecraft firmly ingrained in my head, I wanted to make a post showing off the technical prowess of gamers, displaying the variety of games that you can build a full (but laggy) computer in, along with a little description of Turing machines and their importance in all of this.


## Minecraft (obviously)


Minecraft stands out as the quintessential sandbox game for in-game computer creation. Players have built impressive computing systems using redstone, a game element that functions similarly to electrical circuits. These creations range from fully functional 8-bit computers capable of running basic programs to working graphing calculators and even devices that can play simple games like Tetris or Snake. These redstone computers often use thousands of components and can take months to design and build, showcasing the incredible creativity and problem-solving skills of the Minecraft community.


Redstone works a lot like real life signals, having a high and low version of the signal, and there are machines that can read the signal, like lamps (which act like pixels of a display). Using other redstone components, one can build almost anything, from logic gates like below, to analogs of real life transistors.


<img alt="Redstone diagram" src='https://raw.githubusercontent.com/qerty2006/qerty2006.github.io/refs/heads/main/_site/assets/images/g05ar4oaspt61.webp'/>




Redstone also has its own unique mechanic that we can't utilize as easily in real life; signal strength. Unlike real life, signal strength in Minecraft is discrete, and can be read and produced effectively by  redstone components like comparators. This means with the right circuitry, people have designed machines using this pseudo-analog signal system to make [MIDI inspired music machines] in Minecraft.




<img alt="Redstone signal strength" src='https://raw.githubusercontent.com/qerty2006/qerty2006.github.io/refs/heads/main/_site/assets/images/signal_strength_line.png'/>


If you want to learn more about redstone computing, I cannot recommend anyone more than [Mattbatwings] on Youtube. From [QR code generators] to [basic logic gate explanations], this channel not only showed me how to break servers with computationally complex operations but also gave me the building blocks to understand how regular computer chips work.


<iframe width="560" height="315" src="https://www.youtube.com/embed/osFa7nwHHz4?si=SDxvz2X0Ds1xsVR9" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


## Terraria (aka 2D Minecraft)


I joke about Terraria being just a 2-dimensional version of Minecraft, but its own game with its own unique ways of sending signals: wires, with different colors sending different signals that don't overlap. It even has ways to make [transistors], which are memory preserving circuits essential for real life computers.


<img alt="Redstone signal strength" src='https://raw.githubusercontent.com/qerty2006/qerty2006.github.io/refs/heads/main/_site/assets/images/uoatulrux2m91.webp'/>








A good channel for learning about Terraria circuit making is [From Scratch]'s video on [building a computer in Terraria]. I don't play this game nearly as much as I play Minecraft, so I can't explain as well the amazingness of this process.


<iframe width="560" height="315" src="https://www.youtube.com/embed/zXPiqk0-zDY?si=75Nk72XuoBFZjxGi" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>








## Why did I mention Turing machines before?


At the forefront of all this, the incredibly simple way to answer if you can make a computer in a game, video or otherwise, is one question: Is it Turing Complete?


### What's a Turing Complete System?


Imagine a person who is given a list of numbers written on a paper of arbitrary length. They can do only 3 things with it:


1. Read the symbol at the current spot on the list
2. Write a symbol at the current spot on the list, erasing the previous symbol
3. Move up or down the list a specific amount of times.


Along with this, the person also has a **VERY** long set of instructions which has instructions for every possible combination of position on the list, like


"If you are on the first item of the list and it says '4', change it to 'apple' and move down the list 16 times."


This simple model, known as a Turing machine, is capable of performing any computation that a modern computer can do, and a  system is considered Turing complete if it can simulate this Turing machine using its own built in operations. For example, Minecraft is Turing complete because of its ability to store information in blocks like copper bulbs and rails, and then using that information to change other blocks in a sequence.




## Magic The Gathering (all hail card games)


With this new idea of what games can make computers within them, we can jump out of a computer, and into games of cardboard and paper.




Magic: The Gathering, the popular trading card game, has been proven to be Turing complete, with a full detailed process of how to do so in this [paper], by drawing a very specific set of cards at the beginning of the game, crippling your opponent's ability to play (totally legal play, and technically this uses a deck that was legal in the past), and then going off on your merry way, boosting and dropping the stats of monsters in a "feedtape" displayed on the board. This means that, in theory, it can simulate any computer algorithm. albeit in a highly impractical and complex manner.






<iframe width="560" height="315" src="https://www.youtube.com/embed/pdmODVYPDLA?si=Zzzjbzg5bcfFmIG7" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


Kyle Hill's channel [Because Science] goes through the process of destroying your friendships in Magic, and also explains [how long it would take to complete your cardboard computer.](https://www.youtube.com/watch?v=uDCj-QOp5gE)


# Why should we care?


Though these may just seem like games for children (as a child I will be very disappointed if that is what you believe) the ability to create computers within games has several important implications:




1. **Educational Value:** These in-game computers serve as excellent tools for teaching basic computer science concepts. They provide a visual and interactive way to understand logic gates, circuits, and programming, and for me personally made a lot more sense than many coding classes and textbooks.


2. **Understanding Computational Limits:** By exploring what can be built within these constrained environments, we gain insights into the abstract concept of computation itself and the limits of what computers can do.


3. **Inspiration for Real-World Innovation:** Some of the creative solutions found in these game environments might inspire new approaches to real-world computing problems, maybe even revolutionizing modern computing.




[Mattbatwings]:https://www.youtube.com/c/Mattbatwings
[QR code generators]: https://www.youtube.com/watch?v=ZizmvuZ3EFk
[basic logic gate explanations]: https://www.youtube.com/watch?v=osFa7nwHHz4&t=6s
[MIDI inspired music machines]: https://www.youtube.com/watch?v=V6X2BHpeLww
[transistors]: https://forums.terraria.org/index.php?threads/a-reference-guide-for-simple-logic-devices.81751/
[From Scratch]: https://www.youtube.com/@built-from-scratch
[building a computer in Terraria]: https://www.youtube.com/watch?v=zXPiqk0-zDY&t=204s
[paper]: https://arxiv.org/abs/1904.09828
[Because Science]: https://www.youtube.com/channel/UCvG04Y09q0HExnIjdgaqcDQ

