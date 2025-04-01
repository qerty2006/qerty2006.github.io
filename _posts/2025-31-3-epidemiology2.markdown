---
layout: post
title: "Epidemiology Part 2: My Journey Through simulating a Pandemic"
date: 31-3-2025 00:00:00
categories: math simulation pandemic 
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

After a week of no video games, I attempted to rewrite my outbreak simulator. It sounds simple, but it was a lot of work (hence no Minecraft) and was a ton of fun. Even as I'm writing this introduction, I'm running simulations, and as you read this post, you'll see what new phenomenons stem from a more accurate simulation.

## The Rewrite

Before, the simulator was nowhere near as flexible. Now there are way too many options:

### Incorporating a Complex Virus

One of the significant improvements was the introduction of a more complex virus model. In the improved model, the virus has an incubation period, during which it can still be spread, although at a lower rate. This is a crucial addition, as it more accurately reflects how many viruses, including SARS-CoV-2, behave in the real world.

Key features of the complex virus:

*   **Incubation Period:** The virus now has an incubation period. During this time, individuals are considered "infected" but not "sick" and can still spread the virus.
*   **Vaccination Impact:** If a person is not vaccinated, they will become sick after the incubation period and can only start recovering after becoming sick. However, if vaccinated, a person can start recovering during the incubation period.
*   **Mortality:** Individuals cannot die during the incubation period but can still spread the virus.

### Enhanced Transmission Dynamics

The original simulation used single values, $P_u$ and $P_c$, to represent the probabilities of spreading and catching the virus, respectively. The improved version uses arrays for these values, allowing for more nuanced transmission dynamics. This also extends to the masking effect, which can now be represented as an array.

The transmission dynamics are triggered as follows:

1. **Random Index Selection:** Before calculating masking, a random index of $P_u$ is selected. This index is then used for all subsequent calculations, simulating different modes of interaction such as coughing, sneezing, or direct contact.
2. **Masking Effects:** The masking effects now account for various preventative measures like wearing masks, washing hands, and elbow coughing.
3. **Probability Calculation:** The odds of catching an infection from a sick person on a given day are calculated using the formula:

   $P_u \times P_c \times (1 - (mask_{effectiveness} \text{ if masked else } 0))^2$
   $\times (\text{extra odds based on if the people are immunocompromised, vaccinated, asymptomatic, etc})$

   This formula accounts for the probabilities of spreading and catching the virus, as well as the effectiveness of masks, being vaccinated, asymptomatic, etc.

### Complex Vaccinations

The vaccination model has also been significantly enhanced. The updated version considers two types of vaccines:

*   **Time to Effect:** The model now includes a time component for the vaccine to take effect, after which the person is considered fully vaccinated and receives the full benefits of vaccination.
* **Immunocompromised:** Additionally, the model now includes the ability to simulate the lower odds of immunocompromised people getting vaccinated, also allowing us to see if mass vaccinations can protect people with weakened immune systems.

### Dynamic Outbreak Simulation

To simulate public reaction to the outbreak, the improved model includes the ability for individuals to change their behavior based on the current situation. This adds a layer of complexity, as it allows for the simulation of public health measures and individual responses to the pandemic.

*   **Mask-Wearing:** People can choose to wear masks based on the overall percentage of sick individuals in the population.
*   **Isolation:** Individuals can choose to isolate themselves based on the overall percentage of sick individuals, both when healthy and when sick (resulting in a reduced contact rate).
*   **Vaccination Decisions:** Healthy individuals can choose to get vaccinated based on the overall percentage of sick individuals.

### Public Health Measures

The simulation can now trigger public health measures based on predefined infection thresholds. These measures can significantly impact the course of the simulated pandemic.

*   **Mask Mandate:** When triggered, this measure requires all individuals to wear masks, resulting in a high mask-wearing rate (e.g., 90%).
*   **Total Lockdown:** This measure enforces isolation, leading to a significantly reduced contact rate for both sick and healthy individuals.
*   **Vaccination Campaign:** This measure promotes vaccination, resulting in a high vaccination rate for both short-term and long-term vaccines.

## What New Phenomena Can be Simulated?

### Waves of Infection

The previous iteration made it so once someone recovers from the virus, they cannot catch nor spread the virus anymore, allowing a single wave of infection to occur. In the new version, the virus can continue to spread even after a person recovers, creating multiple waves of infection.

### Testing Government Mandates

Now that we can test the effects of government mandates, we can see how calls to quarantine when sick, vaccinating swaths at the population at a time, and more can affect the spread of the virus.
 
 Now we have a `Government` class, which can force "mandates" to forcibly increase the amount of people isolated, vaccinated, etc.

 ```python
# ... other configuration code ...

default_government_config = {
    "vaccinate_threshold": 0.01, # Government triggers vaccination campaign at 1% infection
    "vaccinate_floor": 0.005, # Mandate deactivates at 0.5%
    "vaccinate_amount": 0.99, # wants everyone to be vaccinated
    "vaccinate_fail": 0.999, # Only 0.001% of unvaccinated people get vaccinated on a given day

    "mask_threshold": 0.1, # Government triggers mask mandate at 10% infection
    "mask_floor": 0.005, # Mandate deactivates at 0.5%
    "mask_amount": 0.99, # wants everyone to wear masks
    "mask_fail": 0.999, # Only 0.001% of unmasked people start wearing masks on a given day

    "isolate_threshold": 0.1, # Government triggers isolation mandate at 10% infection
    "isolate_floor": 0.005, # Mandate deactivates at 0.5%
    "isolate_amount": 0.8, # wants almost everyone to be isolated
    "isolate_fail": 0.999, # Only 0.001% of healthy people start isolating on a given day
    "sick_isolate_fail": 0.01 # If sick, forced to isolate
}

# ... code for simulation setup and execution ...

test_sim_config = {
    # ... other simulation configuration ...
    "government": default_government_config
}
sim = VirusSimulation(test_sim_config, preinstalled=False)

# ... simulation execution code ...
```

For example, I saw that reducing the threshold to trigger the lockdown mandate, as well as enforcing the lockdown better, resulted in half the mortality rate, even with no one initially vaccinated.

|Config|Result|
|---|---|
|The one from above| **Day 100:** **healthy**: 44231 (88.46% of original population) **infected**: 0 (0.00% of original population) **sick**: 1 (0.00% of original population) **recovered**: 37650 (75.30% of original population) **untouched**: 6582 (13.16% of original population) **dead**: 5768 (11.54% of original population)|
|10x more enforced (10x more likely for someone to follow a measure on a given day)|**Day 97:** **healthy**: 44964 (89.93% of original population) **infected**: 0 (0.00% of original population) **sick**: 0 (0.00% of original population) **recovered**: 38392 (76.78% of original population) **untouched**: 6572 (13.14% of original population) **dead**: 5036 (10.07% of original population) |
|Lockdown(almost starts isolating in 2 days)|**Day 83:** **healthy**: 47107 (94.21% of original population) **infected**: 0 (0.00% of original population) **sick**: 0 (0.00% of original population) **recovered**: 31849 (63.70% of original population) **untouched**: 15258 (30.52% of original population) **dead**: 2893 (5.79% of original population)|

Speaking of vaccines, for viruses with vaccines that already exist at the time of an outbreak

|Config|Result|
|---|---|
|No one can be vaccinated, but everyone isolates|**Day 100:** **healthy**: 45757 (91.51% of original population) **infected**: 1 (0.00% of original population) **sick**: 8 (0.02% of original population) **recovered**: 27705 (55.41% of original population) **untouched**: 18060 (36.12% of original population) **dead**: 4234 (8.47% of original population)|
|Everyone isolates, and 50% of people start vaccinated (and a vaccine exist)|**Day 100:** **healthy**: 48881 (97.76% of original population) **infected**: 1 (0.00% of original population) **sick**: 6 (0.01% of original population) **recovered**: 9182 (18.36% of original population) **untouched**: 39705 (79.41% of original population) **dead**: 1112 (2.22% of original population)|
|75% of people are vaccinated, no government intervention|**Day 149:** **healthy**: 48443 (**96.89% of original population**) **infected**: 0 (**0.00% of original population**) **sick**: 0 (**0.00% of original population**) **recovered**: 32267 (**64.53% of original population**) **untouched**: 16176 (**32.35% of original population**) **dead**: 1557 (**3.11% of original population**)|
|99% of able people are vaccinated, no government intervention| No one died, even though people were infected|

This previous example shows the effectiveness of mass vaccinations, especially for those with weakened immune systems. 4% of people in this example were much more susceptible to the virus than others, and yet they had a death rate very similar to the rest of the population.

## The Cost of Simulation

While a model like this could help with simulating an outbreak across UCLA's campus (around 50,000 people), there is a cost we can calculate.

Since we are assuming anyone can connect to anyone else in the network, there is a lot of connections possible. Even by using the more efficient storage method (an adjacency matrix ignoring self-loops) we are storing a lot of data, specifically $\frac{(50,000)*(50,001)}{2}$ bits, or $1,250,025,000$ bits, or $156$ MB of RAM, just for the connection storage. For the entire city of LA (3.82 million), it would take $4$ TB of RAM, and for the US (340 million), it would take $7.25$ MILLION Gigabytes of RAM, or $7.25$ petabytes of RAM. For context, the largest supercomputer in the US, El Capitan, has only $5.4375$ petabytes of RAM. 

It's good that this is only the upper bound for how much RAM will be needed, because there are ways to optimize. For example, you aren't always interacting with people in New York if you live in LA. Some may do that if they repeated go there for work, but there's no point trying to set up connections where its not realistic. Thus it is possible to reduce the amount of RAM needed by making small networks for cities, and then adding a few carrier nodes per city which connect them all together.

## Conclusion

This project was a deep dive into the discrete methods that can be employed to understand the complex dynamics of virus spread within a population. By iteratively enhancing our simulation, we have demonstrated how incorporating details such as incubation periods, dynamic transmission probabilities, behavioral adaptations, and public health mandates can profoundly alter epidemic outcomes. 

The evolution of our simulator,from simple models with fixed probabilities to sophisticated representations involving arrays for nuanced behavior, illustrates that even minor parameter adjustments can lead to significantly different epidemic scenarios. This exploration underscores the power of discrete simulation techniques in mimicking the unpredictable nature of real-world outbreaks.

Moreover, as we push the boundaries with more advanced programming techniques and leverage increasingly powerful hardware, our ability to model and analyze these discrete interactions will only improve. With such advancements, the insights gleaned from simulations will become even more precise, potentially guiding policy decisions and public health strategies with greater accuracy.

In essence, this project serves as a testament to the potential of computational epidemiology: with refined methods and robust computing resources, we can transform theoretical models into actionable insights that help us better predict and control the spread of disease.

Also the code for this is available on [Github](https://github.com/qerty2006/Blog-Post-Code), at `31-3-2025-epi2.py` If you want to try it yourself, add `virussim2.py` to your files and look at the `main.py` and `main2.py` to see examples of the code being used.

