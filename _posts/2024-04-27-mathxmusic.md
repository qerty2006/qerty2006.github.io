---
layout: post
title: "The Intersection of Mathematics, Physics, Psychology, and Music"
date: 27-4-2025 00:00:00
categories: Math Theory
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


Music has long fascinated mathematicians, physicists, and psychologists due to its unique position at the crossroads of measurable phenomena and subjective experience. This post explores how these disciplines converge to explain musical perception, composition, and emotional impact.

### 1. Mathematical Foundations of Musical Structure  
#### Wave Equation and Sound Propagation  
The physics of music begins with the **wave equation**, which governs all acoustic phenomena. For a vibrating string fixed at both ends, the 1D wave equation is:

$$
\frac{\partial^2 y}{\partial t^2} = c^2 \frac{\partial^2 y}{\partial x^2}
$$

where $y(x,t)$ represents string displacement, $c$ is wave speed ($c = \sqrt{T/\rho}$ for tension $T$ and linear density $\rho$), and $x,t$ denote position and time. Solutions to this equation reveal **standing wave patterns** that define musical notes:

$$
y_n(x,t) = \cos\left(\frac{n\pi x}{L}\right)\left[A_{max}\sin\left(\frac{n\pi ct}{L} + \phi\right) \right]
$$

Here, $n$ determines the harmonic number, $L$ is string length, and $A_{max}/\phi$ depend on initial conditions. These normal modes explain why plucked strings produce characteristic timbres containing multiple frequencies:

```python
# Simulating string vibration using wave equation solutions
import numpy as np
import matplotlib.pyplot as plt

L = 1.0       # String length (m)
c = 100.0     # Wave speed (m/s)
n = 3         # Harmonic number
x = np.linspace(0, L, 1000)

# Third harmonic displacement at t=0
y = np.sin(n * np.pi * x / L)
plt.plot(x, y)
plt.title(f'Standing Wave: n={n} Harmonic')
plt.xlabel('Position (m)'); plt.ylabel('Displacement (m)')
plt.show()
```

#### Fourier Analysis and Timbre Decomposition  
Joseph Fourier's breakthrough revealed that any periodic sound can be decomposed into sinusoidal components:

$$
f(t) = \sum_{n=0}^\infty \left[a_n\cos(n\omega t) + b_n\sin(n\omega t)\right]
$$

where coefficients $a_n,b_n$ determine amplitude ratios. This mathematical framework enables modern audio processing, letting engineers analyze instrument spectra much like how astronomers use spectroscopy to determine the composition of celestial bodies. This can allow a more rigorous analysis to determine what makes a saxophone sound different to a trumpet and so on. 

### 2. Psychoacoustics: Bridging Physics and Perception  
#### Critical Bands and Loudness  
Human hearing doesn't perceive all frequencies equally. The ear partitions sounds into **critical bands** - frequency ranges where components interact nonlinearly. Loudness $N$ in sones is calculated through Bark-scale transformations:

$$
N = 0.08\left(\frac{E}{E_0}\right)^{0.23}
$$

where $E$ is sound energy within critical bands and $E_0$ is the reference at 1 kHz. This can help to explain why equal physical intensities don't produce equal perceived loudness across frequencies.

#### Temporal Processing and Rhythm Cognition  
The brain processes rhythmic patterns through coupled oscillator models:

$$
\frac{d\phi}{dt} = \omega + \epsilon \sin(\phi_{ext} - \phi)
$$

where $\phi$ is oscillator phase, $\omega$ natural frequency, and $\epsilon$ coupling strength. This synchronization enables beat perception even with irregular inputs, fundamental to musical enjoyment.

### 3. Emotional Resonance: Where Math Meets Mind  
#### Geometric Foundations of Musical Emotion  
David Lewin's transformational theory models musical tension using group theory:

$$
T_{n,k}(S) = \{s + n + k\cdot12 | s \in S\}
$$

where $T_{n,k}$ represents transposition by $n$ semitones and inversion $k$. Listeners perceive these transformations as emotional trajectories, with major chords (frequency ratio 4:5:6) evoking happiness versus minor chords (10:12:15) suggesting melancholy.

#### Neural Correlates of Musical Pleasure  
fMRI studies show overlapping activation in the prefrontal cortex when processing complex music and solving spatial-temporal math problems. The **nucleus accumbens** shows increased dopamine release during peak emotional moments in music, mirroring responses to mathematical "eureka" moments.

---

From the wave equation's tyranny over vibrating strings to the brain's dance with harmonic complexity, music emerges as nature's grand interdisciplinary laboratory. As David Hilbert once quipped, "Mathematics knows no races or geographic boundaries; for mathematics, the cultural world is one country" - a truth equally valid for the universal language of music.
 
 ---

 Now as I wrote that last part, I was thinking, "Hmm... how does culture influence mathematics? It can clearly influence music, so maybe there could be a case to say culture influences math." That will probably be a pst for next week.... 


**Stuff I Read for this:**

Bark Scale: https://en.wikipedia.org/wiki/Bark_scale

General Intro to Math in Music: https://www.uwlax.edu/globalassets/offices-services/urc/jur-online/pdf/2011/hammond.mth.pdf

Music x Emotion: https://en.wikipedia.org/wiki/Music_and_emotion

