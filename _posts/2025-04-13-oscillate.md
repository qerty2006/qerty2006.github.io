---
layout: post
title: "Beginner's Guide to Oscillations"
date: 13-4-2025 00:00:00
categories: Math Physics
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

My friends often joke about how bad my spelling can be, the worst case being "oscillate"; for the last 3 years, I've always spelled this word incorrectly, only figuring out in my first quarter in college how to remember the correct spelling.

Anyway, now that I'm taking a physics class, I've been learning about oscillations, and I wanted to make a small guide about their derivation and applications.

---

## Oscillations and Damping

### Physical Setup

Consider a spring-mass system with damping:

- **Mass** ($m$): The object attached to the spring.
- **Spring constant** ($k$): Determines the stiffness of the spring.
- **Damping coefficient** ($b$): Represents resistive forces like friction.
- **Displacement** ($x$): Position of the mass relative to equilibrium.
- **Velocity** ($v = \frac{dx}{dt}$): Rate of change of displacement.
- **Acceleration** ($a = \frac{d^2x}{dt^2}$): Rate of change of velocity.

The net force acting on the mass is given by:
$$ F = ma = -kx - bv $$

### Equation of Motion

From Newton's second law:
$$ m\frac{d^2x}{dt^2} + b\frac{dx}{dt} + kx = 0 $$

Define:
$$ \gamma = -\frac{b}{2m}, \quad \omega_0 = \sqrt{\frac{k}{m}} $$

The equation simplifies to:
$$ \frac{d^2x}{dt^2} + 2\gamma\frac{dx}{dt} + \omega_0^2 x = 0 $$

### General Solution ([Check out my post on differential equations to learn how to solve the above equation](https://qerty2006.github.io/math/education/2025/02/22/diffeqs.html))

The solution depends on the relationship between $\gamma$ and $\omega_0$. Let:
$$ x(t) = e^{-\gamma t} \left( C_1 e^{\sqrt{\gamma^2 - \omega_0^2}t} + C_2 e^{-\sqrt{\gamma^2 - \omega_0^2}t} \right) $$

#### Overdamped Case ($\gamma^2 > \omega_0^2$)
$$ x(t) = C_1 e^{\gamma t + \sqrt{\gamma^2 - \omega_0^2}t} + C_2 e^{\gamma t - \sqrt{\gamma^2 - \omega_0^2}t}  $$

$$ x(t) = C_1 e^{t(\gamma + \sqrt{\gamma^2 - \omega_0^2})} 1 + \frac{C_2}{C_1} e^{ -2t \sqrt{\gamma^2 - \omega_0^2}}  )$$

For overdamped cases, the second term can be ignored at large values of $t$, and shows that the displacement $x(t)$ decays exponentially in a manner proportional to $e^{\gamma t + \sqrt{\gamma^2 - \omega_0^2}t}$, the term with an exponent closer to 0. Overdamped cases are more common in nature than underdamped or critically damped cases.



#### Underdamped Case ($\gamma^2 < \omega_0^2$)
$$ x(t) = e^{\gamma t} \left[ C_1 \cos\left(t\sqrt{\omega_0^2 - \gamma^2}\right) + C_2 \sin\left(t\sqrt{\omega_0^2 - \gamma^2}\right) \right] $$

Alternatively:
$$ x(t) = A e^{\gamma t} \cos\left(t\sqrt{\omega_0^2 - \gamma^2} + \phi\right) $$
Where:
$$ A = \sqrt{C_1^2 + C_2^2}, \quad \phi = \arctan\left(\frac{C_1}{C_2}\right) $$

In underdamped cases, you can see something similar to simple harmonic motion; there is a sinusoidal oscillation with a period of $2\pi/\sqrt{\omega_0^2 - \gamma^2}$ and an amplitude of $Ae^{\gamma t}$.


#### Critically Damped Case ($\gamma^2 = \omega_0^2$)
$$ x(t) = e^{\gamma t}(C_1 + C_2 t) $$

At first glance, this looks like the overdamped case, but notably this case has the smallest amount of dampening needed to stop the oscillations, meaning for a given starting point, the critically damped case returns to equilibrium faster than the overdamped case.

## Applications of These scenarios


Underdamped, overdamped, and critically damped systems each serve distinct purposes in engineering and physics, with applications tailored to their unique response characteristics. Below is a detailed breakdown of their use cases:

---

### **Underdamped Systems**  
Characterized by oscillations before settling to equilibrium, underdamped systems prioritize rapid response and controlled vibration absorption.  

**Key Applications**:  
- **Vehicle Suspensions**: Designed to absorb road shocks while maintaining ride comfort. The oscillatory response helps smooth out bumps, though excessive oscillation is mitigated through tuning to be as close to zero as possible.  
- **Electrical Circuits**: Used in filters and amplifiers where frequency selectivity and resonance are critical (e.g., radio receivers).    
- **Seismometers**: Detect ground motion by leveraging underdamped oscillations to record seismic activity accurately.  

---

### **Overdamped Systems**  
These systems return to equilibrium slowly without oscillating, ideal for avoiding overshoot entirely, and extending the time to return to equilibrium.  

**Key Applications**:  
- **Door Closers**: Prevent rapid slamming by gradually returning doors to their closed position; ideal for safety.  
- **Heavy Machinery**: Used in industrial settings where oscillations could damage equipment (e.g., cranes or elevators).  
- **Tuned Mass Dampers in Skyscrapers**: Overdamping stabilizes structures against wind or seismic forces without introducing resonant vibrations; overdamping is used since it can account for the most extreme conditions.  

---

## **Critically Damped Systems**  
Balancing speed and stability, critically damped systems reach equilibrium fastest without oscillation. This can be more difficult to tune compared to underdamped and overdamped systems, but the benefits can be worth it.

**Key Applications**:  
- **Car Shock Absorbers**: Optimized to return wheels to the road surface quickly after bumps, minimizing bounce.  
- **Bathroom Scale Needles**: Ensure immediate settling to display weight without oscillation; bouncing scales aren't fun to use.  


---

### **Comparison of Damping Types**  
| **Parameter**       | **Underdamped**          | **Critically Damped**       | **Overdamped**              |  
|----------------------|--------------------------|-----------------------------|-----------------------------|  
| **Response Time**    | Fast (with oscillations) | Fastest (no oscillations)   | Slow (no oscillations)      |  
| **Overshoot**        | Yes                      | No                          | No                          |  
| **Typical Uses**     | Suspensions, audio EQ    | Shock absorbers, scales     | Door closers, skyscrapers   |  


#### **Conclusion**

Oscillations are cool, and now I can spell "oscillate" correctly!

Yeah there wasn't much to this, but I thought it was interesting for a small post.