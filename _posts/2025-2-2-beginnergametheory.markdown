---
layout: post
title: "Beginner's Guide to Game Theory "
date: 2025-02-02 00:00:00
categories: Math Games Logic 
author: 'Nishanth Tharakan'
---

<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\$$","\$$"] ],
      processEscapes: true
    }
  });
</script>

<script type="text/javascript" charset="utf-8" 
src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML,
https://vincenttam.github.io/javascripts/MathJaxLocal.js"></script>

Game theory is the study of strategic decision-making between rational actors (individuals who given a situation will always pick the situation optimal for them, notably optimizing their strategy regardless of the actions of others). It provides a framework for understanding how individuals or entities make choices when their outcomes depend on the actions of others, and also provides insight into what are considered "equilibriums" in this kind of puzzle.  This post will introduce key concepts in game theory and explore various types of games that model real-world scenarios.

## Four Main Types of Games

1. Chicken Games
2. Battle of Preferences (typically known as Battle of the Sexes)
3. Prisoner's Dilemma
4. Assurance Games

## Chicken Games

In a "chicken" game, two players face off in a high-stakes confrontation where the worst outcome occurs if neither player yields. A classic example is the mutually assured destruction scenario in nuclear deterrence.

Consider two nuclear powers, A and B, each deciding whether to launch a nuclear strike or stand down:

| A / B | Launch | Stand Down |
|-------|--------|------------|
| Launch | (-10, -10) | (5, -5) |
| Stand Down | (-5, 5) | (0, 0) |

In this scenario, mutual destruction (-10, -10) is the worst outcome for both parties (both go negative). The "winner" gains a strategic advantage (5) while the "loser" faces severe consequences (-5). If both stand down, the status quo is maintained (0, 0).

## Battle of Preferences (Battle of the Sexes)

This game models situations where two players prefer different outcomes but would rather coordinate than act independently. Consider a couple deciding between two restaurants:

| Partner A / Partner B | Italian (A prefers) | Chinese (B prefers)|
|-----------------------|---------|---------|
| Italian (A prefers) | (3, 2) | (0, 1) |
| Chinese (B prefers) | (1, 0) | (2, 3) |

Partner A prefers Italian (3), while Partner B prefers Chinese (3). However, both would rather dine together at either restaurant than eat alone (0).

## Prisoner's Dilemma

The prisoner's dilemma is perhaps the most famous game in game theory. It illustrates the conflict between individual and collective interests and how lack of communication can result in group failure merely by acting rationally.

Two suspects are interrogated separately with the following options:

| Prisoner A / Prisoner B | Remain Silent | Confess |
|-------------------------|----------------|---------|
| Remain Silent | (-1, -1) | (-3, 0) |
| Confess | (0, -3) | (-2, -2) |

 Confessing while the other remains silent leads to freedom (0), but mutual confession results in longer sentences (-2, -2) than if both had remained silent (-1, -1). As we'll discuss later, the game always ends with both 

## Assurance Game

Also known as the "Stag Hunt," this game models situations where cooperation leads to the best outcome, but only if all players cooperate[2]. Consider two companies deciding whether to adopt a new technology (like Thunderbolt 4):

| Company A / Company B | Adopt | Don't Adopt |
|------------------------|-------|-------------|
| Adopt | (10, 10) | (0, 5) |
| Don't Adopt | (5, 0) | (5, 5) |

Mutual adoption leads to the highest payoff (10, 10) since everyone is compatible with each other and the technology is an overall benefit, but there's a risk if one company adopts while the other doesn't (0, 5) since there's no point in using a Thunderbolt 4 drive if you have a incompatible port to use with it.

## Nash Equilibrium

A Nash equilibrium occurs when no player can unilaterally improve their outcome (the outcome number they get) by changing their strategy; the cool thing about these equilibriums is that a game can have multiple possible equilibria. For the games above:

- Chicken: Two Nash equilibria - (Launch, Stand Down) and (Stand Down, Launch); unlike how nations would typically react to nukes (or tariffs like in the US and Canada's case right now), a true rational equilibrium occurs when only one side chooses violence. 
- Battle of Preferences: Two Nash equilibria - (Italian, Italian) and (Chinese, Chinese); actually very close to how many couples work in real life, the participants gain more from the company than from the restaurant, so one will cave to the other, and both obtain a net positive.
- Prisoner's Dilemma: One Nash equilibrium - (Confess, Confess); This game is always posed as the reason why rational thought can hurt one's situation rather than help when communication is blocked. In this scenario, Regardless of what B picks, A minimizes time served by staying quiet in both cases: if B confesses, A goes from -3 to -2 by confessing, and if B is silent, A goes from -1 to 0 by snitching.
- Assurance Game: Two Nash equilibria - (Adopt, Adopt) and (Don't Adopt, Don't Adopt); it's pretty simple. If they both don't adopt, status quo is maintained. If they both adopt, status quo is at net benefit for them. At the (Adopt, Don't Adopt) kind of state, it is automatically beneficial for A to not adopt, and for B to adopt, since A goes from 0 to 5, and B goes from 5 to 10.

## Practical Uses of Game Theory

Game theory has wide-ranging applications, with heavy parallels to scenarios in economics and political science, like imposing price changes and tariffs across companies and countries (this does somewhat break down when communication is allowed though). Game theory also has some use in evolutionary biology, where limited communication between species can let us find scenarios very similar to assurance games (I think symbiotic relationships are very similar to assurance games due to the needed universal cooperation requirement).

## Conclusion

Game theory provides powerful tools for analyzing strategic interactions. As we continue to face global challenges requiring cooperation and strategic thinking even in situations of limited communication, the principles of game theory become increasingly relevant in our interconnected world.
