---
layout: post
title: "The Mathematics Behind Epidemiology: Why do Masks, Social Distancing, and Vaccines Work?"
date: 24-3-2025 00:00:00
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

10 days and 5 years ago, I was in 8th grade, finding out that our school was being canceled for a bit due to something called "Covid-19." 1 month turned to 2, turned to 3, and soon turned to 15 months of virtual school. Since March 13th 2020, 704 million caught COVID, and over 7 million died.

In memory of this event that changed the trajectory of my education and the world, I wanted to come back to the basics of epidemiology, and talk about the 3 key things that saved us all: masks, social distancing, and vaccines. Specifically, I wanted to discuss the mathematics behind these important methods of quelling outbreaks, and how their principles can be used to prevent future outbreaks, like measles in the US.

## What is an Epidemic?

An epidemic is defined biologically as the rapid spread of disease exceeding baseline expectations in a population, often driven by factors like pathogen evolution, host immunity changes, or environmental shifts. Mathematically, epidemics are modeled using frameworks like the **SIR model** ($\frac{dS}{dt} = -\beta SI$, $\frac{dI}{dt} = \beta SI - \gamma I$, $\frac{dR}{dt} = \gamma I$), where transmission rate ($\beta$), recovery rate ($\gamma$), and the basic reproduction number ($R_0 = \beta/\gamma$) determine outbreak dynamics. While PDEs (partial differential equations) can be used to model epidemics, I will focus on discrete probability-based models using graphs so more interesting scenarios can be built and tested.

## Intrinsic Factors of Viruses
<table>
  <thead>
    <tr>
      <th>Factor</th>
      <th>Biological Basis</th>
      <th>Mathematical Representation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Susceptibility</strong></td>
      <td>Based both on the soon-to-be host and the pathogen, such as being immune or having a weakened immune system, and the viral load of the pathogen, different viruses have different odds of infecting a host when they enter the host's body.</td>
      <td>For my simulation, this is represented by \(P_c\), the average odds of getting infected by a virus when coming into contact with it.</td>
    </tr>
    <tr>
      <td><strong>Transmission ease</strong></td>
      <td>While the odds of catching the virus depends on the recipient and the virus, the original host plays a vital role in how easily the pathogen spreads, from merely touching something already infected, sneezing, and coughing, or even sex, as is seen with HIV.</td>
      <td>For my simulation, this is represented by \(P_u\), the probability of transmission when two individuals are in contact (this is a mutually independent event to getting infected once in contact with the virus).</td>
    </tr>
    <tr>
      <td><strong>Recovery time</strong></td>
      <td>The length of time a person is infected before fully recovering and thus not transmitting the virus to others; in this scenario, recovery time begins from infection, not from symptoms, one because you can transmit the virus before symptoms appear, and two because some people are asymptomatic and do not show symptoms for the duration of the infection.</td>
      <td>Rather than set a recovery time, I set a recovery probability \(P_r\), which I then use to determine the time until a person recovers.</td>
    </tr>
    <tr>
      <td><strong>Death rate</strong></td>
      <td>The rate at which a person dies from the disease, which is often dependent on age, being immunocompromised, and other factors.</td>
      <td>\(P_k\) is used to determine the probability of death from the disease in a given time step.</td>
    </tr>
    <tr>
      <td><strong>Resistance evolution</strong></td>
      <td>Viruses in real life are not static, but rather evolve over time, often by mutation; as a result, the transmission rate (\(\beta\)) and recovery rate (\(\gamma\)) can change over time as different strains of the same virus evolve and compete to infect people.</td>
      <td>Strain competition equations will help with this, but my simulations do not attempt to model this yet.</td>
    </tr>
  </tbody>
</table>


## The 3 Societal Factors We CAN Change  

While the viruses that cause outbreaks have their own intrinsic factors, the societal factors that we can change during an outbreak (and what we did during the main COVID-19 pandemic) are:

<table>
    <thead>
        <tr>
            <th>Factor</th>
            <th>Biological Basis</th>
            <th>Mathematical Effect</th>
            <th>Mathematical Representation</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><strong>Interactions between people<></strong></td>
            <td>One way to reduce transmission and catching COVID-19 was through social distancing and quarantining; merely reducing contact frequency with others helped us limit the spread of COVID by letting those with the virus fight it before they could spread it to others.</td>
            <td>If society is represented by a graph, where nodes are people and edges are interactions between people, then social distancing and quarantine can be represented by reducing the amount of social contact between people, or cutting edges off the graph. Ultimately, the goal is to quarantine off the effects of a virus, and prevent it from spreading to others, or in this case, lower the odds of a node being a neighbor of an infected node.</td>
            <td>In my simulation, the amount of social contact is determined by the odds of 2 nodes being connected $P_n$, which is a function of social distancing and other measures.</td>
        </tr>
        <tr>
            <td><strong>Barriers for transmission</strong></td>
            <td>When contact cannot be avoided, we still can reduce the odds of transmission through disinfection, masks, and other barriers.</td>
            <td>Mathematically, these barriers act as a new probability game, with the increasing layers of barriers reducing the probability of transmission by a certain amount. For example, if the odds that two people are in contact are $P_u$, and one person wears a mask with an efficacy of $mask_{effectiveness}$, then the probability of transmission is $P_u \cdot (1 - mask_{effectiveness})$. If both wear that same type of mask the odds are $P_u \cdot (1 - mask_{effectiveness})^2$, which is much lower.</td>
            <td>In my simulation, the probability of transmission is reduced by percentage if people masking $P_m$ and their efficacy $mask_{effectiveness}$. This is important because if 2 masked people are in contact, they are less likely to transmit the virus than 2 unmasked people or 1 masked person and 1 unmasked person.</td>
        </tr>
        <tr>
            <td><strong>Vaccines!</strong></td>
            <td>The best way to stop a virus is to prepare the body to fight it; that way, people spend less time infected, are less likely to die, and since they cough and sneeze less, for viruses that rely on airborne transmission, the virus is less likely to spread. Even more importantly, large groups of people getting vaccinated can induce an epidemiological principle called "herd immunity," in which a "herd" of people act as a greater immune system for those who can't get vaccinated (like immunocompromised people) and thus provide protection for them as well.</td>
            <td>In my view on how these vaccines work, they slightly reduce the probability of transmission by a certain amount but definitely reduce the probability of death. as well as increase the probability of recovery. That means people spent less time infected, are less likely to die, and since they cough and sneeze less, for viruses that rely on airborne transmission, the virus is less likely to spread.</td>
            <td>In my simulation, the probability of transmission is reduced by percentage if people are vaccinated $P_v$. Also, I've added a function ${Vaccine}_{function}$ that allows people to be vaccinated over time</td>
        </tr>
    </tbody>
</table>



## My Approach to Simulation

Like I stated earlier, PDEs are a useful tool to model epidemics, but I will focus on discrete probability-based models like using graphs so more interesting models can be built and tested.

I'll be using Python and the [networkx](https://networkx.org/documentation/stable/) library to build the graphs, and good ole fashioned AI to help me program the logic of the simulation:

In a nutshell, the simulation builds a graph of nodes (people) and randomly connects edges (contact between people) to represent people making regular contact. Then people are given the tags [immunocompromised, asymptomatic, vaccinated,] based on the initial config, and then a small number of people are set to be infected.

```python

    def initialize_simulation(self, debug = False) -> None:
        """
        Initializes the simulation graph and attributes for each node.

        The graph is generated using the Erdos-Renyi model with the given
        parameters. Each node is then assigned the following attributes:
        - 'status': Literal['healthy', 'sick', 'recovered', 'dead']
        - 'immunocompromised': bool
        - 'asymptomatic': bool
        - 'vaccinated': bool
        - 'masked': bool

        The initial infected nodes are randomly selected.
        """
        if debug:
            print("Initializing simulation with the following parameters:")
            print(f"Population: {self.N}")
            print(f"Probability of random connection: {self.Pn}")
        self.graph = nx.fast_gnp_random_graph(self.N, self.Pn)
        for node in self.graph.nodes():
            # add code hereto show initilaizing nodes:
            self.graph.nodes[node]['status'] = 'healthy'
            self.graph.nodes[node]['immunocompromised'] = random.random() < self.Pi
            self.graph.nodes[node]['asymptomatic'] = not self.graph.nodes[node]['immunocompromised'] and random.random() < self.Pa
            
            #if immuno compromised, 20% chance of being vaccinated
            if self.graph.nodes[node]['immunocompromised']:
                self.graph.nodes[node]['vaccinated'] = random.random() < self.Pv * 0.2
            else:
                self.graph.nodes[node]['vaccinated'] = random.random() < self.Pv
            

            self.graph.nodes[node]['masked'] = random.random() < self.Pm
            #print(f"Node {node} is {self.graph.nodes[node]}")

        for node in random.sample(list(self.graph.nodes()), self.initial_infected):
            self.graph.nodes[node]['status'] = 'sick'
        if debug:
            print("Simulation initialized")


    

```

Finally, the simulation runs its course. People get vaccinated,infected, recover, and die, and the graph is updated accordingly as the infection "spreads" through the population by reassigning the  node values. 

```python

    def step(self, step: int, debug: bool = False) -> bool:
        """
        Advances the simulation by one step.

        Parameters
        ----------
        step : int
            The current step number.
        debug : bool, optional
            Whether to print debug information. Defaults to False.

        Returns
        -------
        bool
            Whether there are still sick individuals.
        """
        x: int = self.vacfunc(step)
        new_infections: List[int] = []
        new_recoveries: List[int] = []
        new_deaths: List[int] = []
        new_vaccinations: List[int] = []

        for node in self.graph.nodes():
            if self.graph.nodes[node]['status'] == 'sick':

                if random.random() < self.calculate_death_probability(node):
                    new_deaths.append(node)
                elif random.random() < self.calculate_recovery_probability(node):
                    new_recoveries.append(node)
                
                else:
                    for neighbor in self.graph.neighbors(node):
                        if self.graph.nodes[neighbor]['status'] == 'healthy' or self.graph.nodes[neighbor]['status'] == 'recovered':
                            spread_prob: float = self.Pu
                            if self.graph.nodes[node]['vaccinated']:
                                spread_prob /= 2
                            if self.graph.nodes[neighbor]['status'] == 'recovered':
                                spread_prob /= 1000
                            if self.graph.nodes[node]['asymptomatic']:
                                spread_prob /= 2
                            if self.graph.nodes[node]['masked']:
                                if random.random() < self.mask_effectiveness:
                                    continue
                            if self.graph.nodes[neighbor]['masked']:
                                if random.random() < self.mask_effectiveness:
                                    continue
                            if random.random() < spread_prob and random.random() < self.Pc:
                                new_infections.append(neighbor)
        new_vaccinations = random.sample(
            [node for node in self.graph.nodes()
             if not (self.graph.nodes[node]['vaccinated'] and self.graph.nodes[node]['status'] != 'dead')],
            x)

        for node in new_deaths:
            self.graph.nodes[node]['status'] = 'dead'
        for node in new_recoveries:
            self.graph.nodes[node]['status'] = 'recovered'
        for node in new_infections:
            self.graph.nodes[node]['status'] = 'sick'
        for node in new_vaccinations:
            self.graph.nodes[node]['vaccinated'] = True

        current_status: Dict[str, int] = {
            'healthy': 0,
            'sick': 0,
            'recovered': 0,
            'dead': 0,
            'vaccinated': 0
        }
        for node in self.graph.nodes():
            current_status[self.graph.nodes[node]['status']] += 1
            if self.graph.nodes[node]['vaccinated']:
                current_status['vaccinated'] += 1

        self.stats['healthy'].append(current_status['healthy'])
        self.stats['sick'].append(current_status['sick'])
        self.stats['vaccinated'].append(current_status['vaccinated'])
        self.stats['recovered'].append(current_status['recovered'])
        self.stats['dead'].append(current_status['dead'])

        if debug: time.sleep(0.01)
        return current_status['sick'] > 0

```

For statistical purposes, I track the number of healthy, sick, recovered, dead, and vaccinated people in the population over time, as well as run a given configuration 50 times to get an average of the results and see if there is a statistically significant difference.

```python

def runmultisim(config, num_simulations, debug=False):
    print("Initializing simulation")
    total_stats = {
        'steps': [],
        'healthy': [],
        'sick': [],
        'vaccinated': [],
        'recovered': [],
        'dead': [],
        'percentage_survived': [],
        'percentage_died': [],
        'percentage_untouched': [],
        'percentage_immunocompromised_survived': [],
        'percentage_vaccinated_survived': [],
        'percentage_unvaccinated_survived': [],
        
    }
    for i in range(num_simulations):
        sim = VirusSimulation(config)
        steps, stats = sim.run_simulation(max_steps=1000, iteration=i, debug=debug)
        final_stats = sim.print_final_report(i = i)
        for key, value in final_stats.items():
            total_stats[key].append(value)
    os.system('cls' if os.name == 'nt' else 'clear') # Clear console
    for key, value in total_stats.items():
        if "percentage" in key:
            print(f"{key}: {sum(value)/len(value):.2f}%")
        else:
            print(f"{key}: {sum(value)/len(value):.2f}")
    print("Simulation completed")

    # append average of each stat at the end
    for key, value in total_stats.items():
        total_stats[key].append(sum(value)/len(value))
    #set the day of the last one to 999
    #total_stats['steps'][-1] *= num_simulations
    return total_stats

```

The full code can be viewed at [my new GitHub dedicated to blog post related code.](https://github.com/qerty2006/Blog-Post-Code)

Here are some results where I ran simulations on my college campus, assuming no one is vaccinated and no one is wearing masks.:

<div align="center">
<table>
<tr>
    <th>Config</th>
    <th>Results</th>
  </tr>
  <tr>
    <td>
      <pre><code class="python">
defaultconfig = {
    'name': 'default',
    'N': 50000,  # Number of people at UCLA, it's a big campus
    'Pn': 0.0075,  # Probability of a random connection between two people
    'Pi': 0.01,  # Probability of a person being immunocompromised
    'Pv': 0.0,  # Probability of a person initially vaccinated
    'Pa': 0.25,  # Probability of a person being asymptomatic to the virus
    'Pm': 0.005,  # Probability of a person wearing a mask
    'mask_effectiveness': 0.8,  # Average effectiveness of masks
    'initial_infected': 10,  # Number of initially infected people
    'Pu': 0.5,  # Probability of a person spreading the virus
    'Pc': 0.15,  # Probability of a person catching the virus
    'Pk': 0.015,  # Probability of a person dying on a given day
    'Pr': 0.14,  # Probability of a person recovering on a given day
    'Vaccine function': lambda step: 0  # No new vaccinations
}
      </code></pre>
    </td>
    <td>
      <pre><code class="python">
Average days per simulation: 80.02
Average healthy people at the end: 0.0
Average vaccinated people at the end: 0.0
Average recovered people at the end: 45135.46
Average dead people at the end: 4864.54
percentage_survived: 90.27%
percentage_died: 9.73%
percentage_untouched: 0.0%
percentage_immunocompromised_survived: 35.22%
percentage_vaccinated_survived: 0.0%
percentage_unvaccinated_survived: 90.27%
      </code></pre>
    </td>
  </tr>
</table>
</div>

So far, the results are pretty bad, with almost a tenth of the population dying (That's half of my year gone! ). As expected, people who are immunocompromised are the most likely to die with only 35% surviving.

Let's see how the results change if we change some social aspects, like vaccinations, interaction frequency, and masks:

### Masking
<table>
<tr>
    <th>Config</th>
    <th>Results</th>
  </tr>
  <tr>
    <td>
      <pre><code class="python">
# Masking 25%
quartermask = copy.deepcopy(defaultconfig)
quartermask['Pm'] = 0.25
quartermask["name"] = "quartermask"
      </code></pre>
    </td>
    <td>
      <pre><code class="python">
Average days per simulation: 78.12
Average healthy people at the end: 0.0
Average vaccinated people at the end: 0.0
Average recovered people at the end: 45219.92
Average dead people at the end: 4780.08
percentage_survived: 90.44%
percentage_died: 9.56%
percentage_untouched: 0.0%
percentage_immunocompromised_survived: 35.37%
percentage_vaccinated_survived: 0.0%
percentage_unvaccinated_survived: 90.44%
      </code></pre>
    </td>
  </tr>
  <tr>
    <td>
      <pre><code class="python">
# Masking 50%
halfmask = copy.deepcopy(defaultconfig)
halfmask['Pm'] = 0.5
halfmask["name"] = "halfmask"
      </code></pre>
    </td>
    <td>
      <pre><code class="python">
Average days per simulation: 78.34
Average healthy people at the end: 0.02
Average vaccinated people at the end: 0.0
Average recovered people at the end: 45316.1
Average dead people at the end: 4683.88
percentage_survived: 90.63%
percentage_died: 9.37%
percentage_untouched: 0.0%
percentage_immunocompromised_survived: 36.62%
percentage_vaccinated_survived: 0.0%
percentage_unvaccinated_survived: 90.63%
      </code></pre>
    </td>
  </tr>
  <tr>
    <td>
      <pre><code class="python">
# Masking 75%
threefourthsmask = copy.deepcopy(defaultconfig)
threefourthsmask['Pm'] = 0.75
threefourthsmask["name"] = "threefourthsmask"
      </code></pre>
    </td>
    <td>
      <pre><code class="python">
Average days per simulation: 94.0
Average healthy people at the end: 0.5
Average sick people at the end: 0.0
Average vaccinated people at the end: 0.0
Average recovered people at the end: 45350.5
Average dead people at the end: 4649.0
percentage_survived: 90.702%
percentage_died: 9.298%
percentage_untouched: 0.001%
percentage_immunocompromised_survived: 35.394746314349696%
percentage_vaccinated_survived: 0.0%
percentage_unvaccinated_survived: 90.702%
      </code></pre>
    </td>
  </tr>
  <tr>
    <td>
      <pre><code class="python">
# Masking 99%
nineninemask = copy.deepcopy(defaultconfig)
nineninemask['Pm'] = 0.99
nineninemask["name"] = "nineninemask"
      </code></pre>
    </td>
    <td>
      <pre><code class="python">
Average days per simulation: 89.13
Average healthy people at the end: 179.03
Average sick people at the end: 0.0
Average vaccinated people at the end: 0.0
Average recovered people at the end: 45223.17
Average dead people at the end: 4597.8
percentage_survived: 90.8%
percentage_died: 9.2%
percentage_untouched: 0.36%
percentage_immunocompromised_survived: 36.9%
percentage_vaccinated_survived: 0.0%
percentage_unvaccinated_survived: 90.8%
      </code></pre>
    </td>
  </tr>
</table>

Increasing mask usage showed a gradual improvement in outcomes:

- 25% masking reduced deaths from 9.73% to 9.56%
- 50% masking further reduced deaths to 9.37%
- 75% masking brought deaths down to 9.298%
- 99% masking achieved 9.2% deaths and 0.36% untouched population

While masking alone didn't dramatically change outcomes, it did show consistent improvements, even resulting in some people never contracting the virus.

### Isolation
<table>
  <tr>
    <th>Config</th>
    <th>Results</th>
  </tr>
  <tr>
    <td>
      <pre><code class="python">
# Half as many interactions
halfisolation = copy.deepcopy(defaultconfig)
halfisolation['Pn'] /= 2
halfisolation["name"] = "halfisolation"
      </code></pre>
    </td>
    <td>
      <pre><code class="python">
Average days per simulation: 76.5
Average healthy people at the end: 0.0
Average sick people at the end: 0.0
Average vaccinated people at the end: 0.0
Average recovered people at the end: 45324.0
Average dead people at the end: 4676.0
percentage_survived: 90.648%
percentage_died: 9.352%
percentage_untouched: 0.0%
percentage_immunocompromised_survived: 35.837%
percentage_vaccinated_survived: 0.0%
percentage_unvaccinated_survived: 90.648%
      </code></pre>
    </td>
  </tr>
  <tr>
    <td>
      <pre><code class="python">
# Quarter as many interactions
quarterisolation = copy.deepcopy(defaultconfig)
quarterisolation['Pn'] /= 4
quarterisolation["name"] = "quarterisolation"
      </code></pre>
    </td>
    <td>
      <pre><code class="python">
Average days per simulation: 79.77
Average healthy people at the end: 0.27
Average sick people at the end: 0.0
Average vaccinated people at the end: 0.0
Average recovered people at the end: 45356.43
Average dead people at the end: 4643.3
percentage_survived: 90.7134%
percentage_died: 9.2866%
percentage_untouched: 0.0005%
percentage_immunocompromised_survived: 35.876%
percentage_vaccinated_survived: 0.0%
percentage_unvaccinated_survived: 90.7134%
      </code></pre>
    </td>
  </tr>
  <tr>
    <td>
      <pre><code class="python">
# Tenth as many interactions
tenthisolation = copy.deepcopy(defaultconfig)
tenthisolation['Pn'] /= 10
tenthisolation["name"] = "tenthisolation"
      </code></pre>
    </td>
    <td>
      <pre><code class="python">
Average days per simulation: 78.6
Average healthy people at the end: 23.033333333333335
Average sick people at the end: 0.0
Average vaccinated people at the end: 0.0
Average recovered people at the end: 45350.566666666666
Average dead people at the end: 4626.4
percentage_survived: 90.7472%
percentage_died: 9.2528%
percentage_untouched: 0.04606666666666667%
percentage_immunocompromised_survived: 36.22363484762301%
percentage_vaccinated_survived: 0.0%
percentage_unvaccinated_survived: 90.7472%
      </code></pre>
    </td>
  </tr>
</table>

Reducing social interactions had a noticeable impact even with just half the normal interaction rate, but increasing the number of interactions reduced the number of deaths at a slower rate.:

- Halving interactions reduced deaths to 9.352%
- Quartering interactions further reduced deaths to 9.2866%
- Reducing interactions to 1/10th achieved 9.2528% deaths and 0.046% untouched population

Social isolation proved more effective than masking alone, particularly in preserving a small portion of the population from infection, but at the human cost of not being as social.

### Vaccinations
<table>
  <tr>
    <th>Config</th>
    <th>Results</th>
  </tr>
  <tr>
    <td>
      <pre><code class="python">
# 50% vaccinated
halfvacconfig = copy.deepcopy(defaultconfig)
halfvacconfig['Pv'] = 0.5
halfvacconfig["name"] = "halfvacconfig"
      </code></pre>
    </td>
    <td>
      <pre><code class="python">
Average days per simulation: 71.83
Average healthy people at the end: 1666.33
Average sick people at the end: 0.0
Average vaccinated people at the end: 24812.97
Average recovered people at the end: 45866.2
Average dead people at the end: 2467.47
percentage_survived: 95.0651%
percentage_died: 4.9349%
percentage_untouched: 3.3327%
percentage_immunocompromised_survived: 44.6672%
percentage_vaccinated_survived: 99.8021%
percentage_unvaccinated_survived: 90.3979%
      </code></pre>
    </td>
  </tr>
  <tr>
    <td>
      <pre><code class="python">
# 75% vaccinated
threefourthsvacconfig = copy.deepcopy(defaultconfig)
threefourthsvacconfig['Pv'] = 0.75
threefourthsvacconfig["name"] = "threefourthsvacconfig"
      </code></pre>
    </td>
    <td>
      <pre><code class="python">
Results:
Average days per simulation: 56.0
Average healthy people at the end: 0.0
Average sick people at the end: 0.0
Average vaccinated people at the end: 37127.0
Average recovered people at the end: 48554.0
Average dead people at the end: 1446.0
percentage_survived: 97.108%
percentage_died: 2.892%
percentage_untouched: 0.0%
percentage_immunocompromised_survived: 47.77%
percentage_vaccinated_survived: 99.81%
percentage_unvaccinated_survived: 89.31%
      </code></pre>
    </td>
  </tr>
  <tr>
    <td>
      <pre><code class="python">
# 99% vaccinated
nineninevacconfig = copy.deepcopy(defaultconfig)
nineninevacconfig['Pv'] = 0.99
nineninevacconfig["name"] = "nineninevacconfig"
      </code></pre>
    </td>
    <td>
      <pre><code class="python">
Average days per simulation: 55.5
Average healthy people at the end: 89.0
Average sick people at the end: 0.0
Average vaccinated people at the end: 49139.5
Average recovered people at the end: 49537.5
Average dead people at the end: 373.5
percentage_survived: 99.253%
percentage_died: 0.747%
percentage_untouched: 0.178%
percentage_immunocompromised_survived: 50.98%
percentage_vaccinated_survived: 99.79%
percentage_unvaccinated_survived: 68.77%
      </code></pre>
    </td>
  </tr>
</table>

Vaccination showed the most significant impact:

- 50% vaccination reduced deaths to 4.9349%, with 95.065% of vaccinated individuals surviving

- 75% vaccination dramatically reduced deaths to 2.892%, with 97.108% of vaccinated individuals surviving

- 99% vaccination further reduced deaths to 0.747%, with 99.253% of vaccinated individuals surviving, and even 50.98% of immunocompromised individuals surviving

Vaccination not only reduced overall deaths but also significantly protected both vaccinated and unvaccinated populations through herd immunity.
What was even more surprising to me was that even though I gave immunocompromised people a 20% the normal vaccination rate (the reason being some effective vaccines cannot be given to people with weakened immune systems and I wanted to reflect an extreme of that situation: a live vaccine with long lasting effects), as the vaccination rate increase, the herd immunity effect came into being and protected both immunocompromised and unimmunocompromised populations.


### Combos of Vaccinations, Masks, and Social Distancing
<table>
  <tr>
    <th>Config</th>
    <th>Results</th>
  </tr>
  <tr>
    <td>
      <pre><code class="python">
# Combo: 75% masks and 75% vaccination
threefourthsvacmaskconfig = copy.deepcopy(defaultconfig)
threefourthsvacmaskconfig['Pm'] = 0.75
threefourthsvacmaskconfig['Pv'] = 0.75
threefourthsvacmaskconfig['name'] = "threefourthsvacmaskconfig"
      </code></pre>
    </td>
    <td>
      <pre><code class="python">
Average days per simulation: 70.5
Average healthy people at the end: 1852.0
Average sick people at the end: 0.0
Average vaccinated people at the end: 37097.5
Average recovered people at the end: 46775.5
Average dead people at the end: 1372.5
percentage_survived: 97.255%
percentage_died: 2.745%
percentage_untouched: 3.704%
percentage_immunocompromised_survived: 46.436%
percentage_vaccinated_survived: 99.810%
percentage_unvaccinated_survived: 89.910%
      </code></pre>
    </td>
  </tr>
</table>
This combo shows what a potential recurrence of Covid could look like on UCLA's campus, if many people (more than 15k) aren't up to date on their vaccinations, but people still decide to mask up as they go to class. Realistically, UCLA would swap to online classes, but this is just an example of what a potential scenario could look like.


<table>
  <tr>
    <th>Config</th>
    <th>Results</th>
  </tr>
  <tr>
    <td>
      <pre><code class="python">
# Combo: Tenth Isolation and 80% masking
tenthisolationmaskconfig = copy.deepcopy(defaultconfig)
tenthisolationmaskconfig['Pm'] = 0.8
tenthisolationmaskconfig['Pn'] /= 10
tenthisolationmaskconfig['name'] = "tenthisolationmaskconfig"
      </code></pre>
    </td>
    <td>
      <pre><code class="python">
Average days per simulation: 119.5
Average healthy people at the end: 20253.0
Average sick people at the end: 0.0
Average vaccinated people at the end: 0.0
Average recovered people at the end: 27034.5
Average dead people at the end: 2712.5
percentage_survived: 94.575%
percentage_died: 5.425%
percentage_untouched: 40.506%
percentage_immunocompromised_survived: 63.35080645161291%
percentage_vaccinated_survived: 0.0%
percentage_unvaccinated_survived: 94.575%
      </code></pre>
    </td>
  </tr>
</table>
What's important about vaccines is that they take time to make, meaning for a period of time, there is still a high chance of infections. A scenario like pre-vaccine Covid is a good example of this, where we relied on lowered interactions with the outside world, and using masks where we can to minimize risk when doing essential tasks like working or getting groceries.
Notice with no vaccine, with good preparation, and good social distancing, we can prevent a large number of infections, with the a great deal of people not even being infected.

<table>
  <tr>
    <th>Config</th>
    <th>Results</th>
  </tr>
  <tr>
    <td>
      <pre><code class="python">
# Covid combo: 75% vaccination, 75% masking, Tenth isolation
covidcomboconfig = copy.deepcopy(defaultconfig)
covidcomboconfig['Pm'] = 0.75
covidcomboconfig['Pv'] = 0.75
covidcomboconfig['Pn'] /= 10
covidcomboconfig['name'] = "covidcomboconfig"
      </code></pre>
    </td>
    <td>
      <pre><code class="python">
Results:
Average days per simulation: 165.17
Average healthy people at the end: 49984.0
Average sick people at the end: 0.0
Average vaccinated people at the end: 37303.0
Average recovered people at the end: 16.0
Average dead people at the end: 0.0
percentage_survived: 100.0%
percentage_died: 0.0%
percentage_untouched: 100.0%
percentage_immunocompromised_survived: 99.968%
percentage_vaccinated_survived: 100.0%
percentage_unvaccinated_survived: 100.0%
      </code></pre>
    </td>
  </tr>
</table>

I was incredibly shocked by the combination of  vaccine, masks, and isolation, which resulted in a 100% survival rate, so I gave the simulation a stronger virus to deal with:

<table>
  <tr>
    <th>Config</th>
    <th>Results</th>
  </tr>
  <tr>
    <td>
      <pre><code class="python">
#Same social ascepts, but the virus is more contagious
strongercovidcomboconfig = copy.deepcopy(defaultconfig)
strongercovidcomboconfig['Pm'] = 0.75
strongercovidcomboconfig['Pv'] = 0.75
strongercovidcomboconfig['Pn'] /= 10
strongercovidcomboconfig['Pc'] = 0.8 # 80% chance of getting infected if someone comes into contact
strongercovidcomboconfig['name'] = "strongercovidcomboconfig"
      </code></pre>
    </td>
    <td>
      <pre><code class="python">
Results: 
Average days per simulation: 74.03
Average healthy people at the end: 18374.0
Average sick people at the end: 0.0
Average vaccinated people at the end: 37210.03
Average recovered people at the end: 30735.13
Average dead people at the end: 890.97
percentage_survived: 98.22%
percentage_died: 1.78%
percentage_untouched: 36.75%
percentage_immunocompromised_survived: 65.54%
percentage_vaccinated_survived: 99.88%
percentage_unvaccinated_survived: 93.39%
      </code></pre>
    </td>
  </tr>
</table>

Even with this stronger virus, we can still prevent a large number of infections, with the a great deal of people not even being infected.
So what happens when we don't has as strict policies?

<table>
  <tr>
    <th>Config</th>
    <th>Results</th>
  </tr>
  <tr>
    <td>
      <pre><code class="python">
# Same social ascepts, but the virus is more contagious, and vaccination rate is higher
evenstrongercovidcomboconfig = copy.deepcopy(defaultconfig)
evenstrongercovidcomboconfig['Pm'] = 0.25
evenstrongercovidcomboconfig['Pv'] = 0.99
evenstrongercovidcomboconfig['Pn'] /= 1.5
evenstrongercovidcomboconfig['Pc'] = 0.8
evenstrongercovidcomboconfig['Pk'] = 0.03
evenstrongercovidcomboconfig['Pr'] = 0.1
evenstrongercovidcomboconfig['name'] = "evenstrongercovidcomboconfig"
      </code></pre>
    </td>
    <td>
      <pre><code class="python">
Results:
Average days per simulation: 57.0
Average healthy people at the end: 3.77
Average sick people at the end: 0.0
Average vaccinated people at the end: 49100.17
Average recovered people at the end: 49287.1
Average dead people at the end: 709.13
percentage_survived: 98.582%
percentage_died: 1.418%
percentage_untouched: 0.008%
percentage_immunocompromised_survived: 30.762%
percentage_vaccinated_survived: 99.451%
percentage_unvaccinated_survived: 51.179%
      </code></pre>
    </td>
  </tr>
</table>

The results matched my initial thoughts, though not by as much as I originally imagined:

Even with a more aggressive virus and relaxed social distancing measures, the high vaccination rate (99%) still provided significant protection to the population. The overall survival rate remained high at 98.582%, with only 1.418% mortality. This demonstrates the power of widespread vaccination in controlling outbreaks, even when other preventive measures are less strictly followed.

However, some important nuances emerged:

- The unvaccinated population was significantly more vulnerable, with only 51.179% surviving compared to 99.451% of the vaccinated group. This highlights the critical importance of achieving high vaccination rates to protect those who cannot be vaccinated.

- Immunocompromised individuals were still at higher risk, with only 30.762% surviving. This underscores the need for additional protective measures for vulnerable populations, even in highly vaccinated communities.

- Very few people (0.008%) remained untouched by the virus, indicating that high transmissibility can still lead to widespread infection despite precautions.

- The shorter average simulation duration (57 days) suggests that the virus so read quickly through the population, emphasizing the importance of rapid response and preventive measures in the early stages of an outbreak.

These results reinforce the effectiveness of a multi-faceted approach to disease control, combining high vaccination rates with other preventive measures like masking and some degree of social distancing. While vaccines prove to be the most powerful tool, they work best in conjunction with other strategies, especially to protect the most vulnerable members of the population.

## Time for a Part 2!

Unlike my other posts, I actually have time this week to go more in depth with this project, and I want to see how I can build a more complex model to better simulate realistic scenarios.

### Things to include for Part 2:

- **More complex transmission dynamics**: Instead of just one overall transmission method, account for multiple transmission channels, such as respiratory droplets, contact via proxy objects, or direct contact. This way, we can test various individual methods for how one can protect themselves from viruses, from masking to simply washing their hands regularly.

- **More dynamic responses to outbreak**: People notice when things go wrong, and will often react on their own. I want to see if we can simulate a society going from a normal interaction frequency to a lower one, and see how that affects the spread of the virus.

- **More complex vaccinations**: There are multiple types of vaccines, each with their own properties on effectiveness and duration of effect. This also affects who can be vaccinated, and how long they are protected from the virus.

- Probably won't happen: Strain evolution and competition. I'm not sure how to simulate this, it would be interesting. During Covid, we had multiple waves due to different strains having different effects (even with some being more resistant to certain vaccines), and I want to see if we can simulate this in our models.

Part 2 will be posted **here** when it's ready, but until then, please check out the new [GitHub repository]((https://github.com/qerty2006/Blog-Post-Code)) if you want to see the code for this project, as well as the code for my previous posts.

