---
layout: post
title: "Why Math Makes Poker Fun (Sometimes)"
date: 2025-01-11 22:00:00
categories: Math Computer_Science Gambling Game_Theory
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

Poker is a game of skill, strategy, and probability. While many players focus on the bluffing and not revealing your hand side of poker, understanding the basic math behind poker and card counting can give players a significant edge. In this post, we'll explore some fundamental probability concepts in poker and how peeking at cards can dramatically alter the odds.

# How Poker Works

In Texas Hold'em, the most popular variant of poker, each player is dealt two private cards (hole cards) and uses them in combination with five community cards to make the best possible five-card hand. The community cards are revealed in three stages:

1. The Flop: First three community cards
2. The Turn: Fourth community card
3. The River: Fifth and final community card

Players bet after each stage, with the option to check, bet, call, raise, or fold.

What's important is that you have two cards you know of, 5 cards evryone knows of, and you **don't** know the other players' hole cards. In games like poker, information is one of the most essential factors when making a descision.

## Basic Probability Example

Let's consider the probability of getting at least one pair by the end of the hand (after seeing all 7 cards - 2 hole cards and 5 community cards).

The probability of getting at least one pair in a 7-card poker hand is:

$$P(\text{at least one pair}) = 1 - P(\text{no pairs})$$

To calculate this, we need to find the number of ways to select 7 cards with no pairs divided by the total number of possible 7-card hands:

$$P(\text{no pairs}) = \frac{\binom{13}{7} \cdot 4^7}{\binom{52}{7}}$$

Where: 
- $\binom{13}{7}$ is the number of ways to select 7 different ranks

- $4^7$ is the number of ways to select suits for each rank

- $\binom{52}{7}$ is the total number of possible 7-card hands



Calculating this:

$$P(\text{no pairs}) \approx 0.174$$

Therefore:

$$P(\text{at least one pair}) = 1 - 0.174 = 0.826$$

So, the probability of getting at least one pair in a 7-card poker hand is about 82.6%.

## The Impact of Peeking

Now, let's consider what happens if a dealer peeks at the bottom card of the deck before dealing. This seemingly small action can have a significant impact on the game.

Suppose the dealer peeks and sees an Ace at the bottom of the deck. This information changes the probability calculations for everyone at the table, but only the dealer knows it.

For example, if the dealer has a pair of Kings in their hole cards, knowing an Ace is at the bottom of the deck reduces the probability of an opponent having an Ace. The probability of an opponent having at least one Ace changes from:

$$P(\text{at least one Ace}) = 1 - \left(\frac{48}{52} \cdot \frac{47}{51}\right) \approx 0.151$$

to:

$$P(\text{at least one Ace : Ace at bottom}) = 1 - \left(\frac{47}{51} \cdot \frac{46}{50}\right) \approx 0.117$$


This reduction in probability might seem small, but in a game where small edges can lead to significant profits over time, it's a considerable advantage.

Moreover, the dealer could use this information to make more informed decisions about betting, potentially leading to unfair gains. For instance, if the dealer sees a potential Ace-high straight in play, knowing that at least one less person can have an Ace can make them bet more aggressively.

# Real World Scenario

Let's continue with a specific scenario involving Alice and Bob playing Texas Hold'em poker, where Bob accidentally sees the burn card before the flop.

### The Setup

- Alice is the dealer
- Bob is the only other player
- The game is heads-up Texas Hold'em

### The Deal

1. Alice deals the hole cards:
   - Alice's hole cards: K♠ Q♥
   - Bob's hole cards: 8♣ 8♦

2. Alice burns the top card before the flop, but Bob accidentally sees it:
   - Burn card: A♥

3. Alice then deals the flop:
   - Flop: 7♠ J♦ 2♣

### The Calculations

Let's calculate how this information affects the probabilities and decision-making for both players.

#### Bob's Perspective

Bob knows that the A♥ is out of play. This information changes his odds significantly:

1. Probability of Alice having an Ace:
   
   Without seeing the burn card: 
   $$P(\text{Alice has an Ace}) = 1 - \frac{\binom{48}{2}}{\binom{50}{2}} \approx 0.1552$$

   After seeing the burn card:
   $$P(\text{Alice has an Ace}) = 1 - \frac{\binom{47}{2}}{\binom{49}{2}} \approx  0.1224$$

   This is a significant decrease in the probability that Alice has an Ace.

2. Probability of an Ace appearing on the turn or river:
   
   Without seeing the burn card:
   $$P(\text{Ace on turn or river}) = 1 - \frac{\binom{47}{2}}{\binom{50}{2}} \approx 0.1176$$

   After seeing the burn card:
   $$P(\text{Ace on turn or river}) = 1 - \frac{\binom{46}{2}}{\binom{49}{2}} \approx 0.0918$$

   Bob now knows there's a lower chance of an Ace appearing, which could be crucial if he decides to bluff representing an Ace.

#### Alice's Perspective

Alice doesn't know about the burn card, so her calculations remain unchanged. She's playing with incomplete information compared to Bob.

### The Impact on Play

1. Bob's Decision Making:
   - Bob knows his pair of 8s is more likely to be the best hand, as the chance of Alice having an Ace (which would give her a higher pair) is reduced.
   - He might be more inclined to bet aggressively, especially if an Ace doesn't appear on the turn or river.

2. Alice's Misconception:
   - Alice might overestimate the chance of Bob having an Ace or the likelihood of an Ace appearing on later streets.
   - This could lead her to play more cautiously than necessary, potentially missing value with her K♠ Q♥.

Let's continue the scenario with Alice and Bob, now focusing on the turn card and its impact on the game.

## The Next Turn

Alice burns another card before dealing the turn, but this time, she accidentally sees it:

- Burn card: K♣ (seen by Alice)
- Turn card: 9♥

## Updated Calculations

### Alice's Perspective

Alice now has additional information that affects her decision-making:

1. Probability of Bob having a King:

Without seeing the burn card:
$$P(\text{Bob has a King}) = 1 - \frac{\binom{47}{2}}{\binom{49}{2}} \approx 0.1224$$

After seeing the burn card:
$$P(\text{Bob has a King}) = 1 - \frac{\binom{46}{2}}{\binom{48}{2}} \approx 0.0918$$

This significant decrease in probability makes Alice more confident in the strength of her K♠.

2. Probability of a King appearing on the river:

Without seeing the burn card:
$$P(\text{King on river}) = \frac{2}{47} \approx 0.0426$$

After seeing the burn card:
$$P(\text{King on river}) = \frac{1}{46} \approx 0.0217$$

Alice now knows there's a lower chance of improving to three-of-a-kind.

### Bob's Perspective

Bob's calculations remain unchanged from the flop, as he doesn't have new information. However, the 9♥ on the turn gives him additional outs for a straight.

## The Impact on Play

1. Alice's Decision Making:
   - Alice might be more inclined to bet aggressively with her pair of Kings, knowing it's less likely Bob has a King.
   - She's also aware that her chances of improving to three-of-a-kind are lower than Bob might think.

2. Bob's Position:
   - Bob still has his pair of 8s and now has an open-ended straight draw (6 and 10 would complete a straight).
   - He doesn't know about the burned K♣, so he might overestimate Alice's chances of having a King or improving to three-of-a-kind.

## Probability Calculations for Bob's Straight Draw

Bob now has 8 outs for his straight (4 sixes and 4 tens). Let's calculate his odds of hitting the straight on the river:

$$P(\text{Straight on river}) = \frac{8}{46} \approx 0.1739$$

This gives Bob about a 17.39% chance of hitting his straight on the river.

## Ethical Considerations

Both players now have information they shouldn't have. In a fair game, they should have reported seeing the burn cards, resulting in a misdeal. This scenario highlights how easily the integrity of the game can be compromised, even unintentionally.

# Conclusion

This extended scenario demonstrates how hidden information can significantly impact poker probabilities and decision-making. It underscores the importance of maintaining game integrity and the complex calculations players must consider, often with incomplete information. In real-world poker, the ability to make accurate probability assessments under uncertainty is a crucial skill that separates skilled players from novices.

### My PyPoker Project
If you want to test out cheating poker strategies while not in a real game, I'm working on a Python library that lets you play Poker from the terminal from scratch. It's been a long progress trying to come up with a nice way to calculate the value of a particular hand, and before you say to use a lookup table, remember there's over 100 million unique poker hands (52 choose 7 is huge) and the lookup table could take up its own SSD on your computer. Trust me, I almost bricked my Macbook Air running a program to do so, and within 10 minutes the computer was using 20 GB of swap... anyway check it out here: https://github.com/qerty2006/PyPoker and let me know what you think!



