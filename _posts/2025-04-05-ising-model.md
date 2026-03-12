---
layout: page
title: The Ising Model and Phase Transitions
date: 2025-04-05 11:00:00-0400
description: Statistical mechanics of the Ising model, mean-field theory, and the ferromagnetic phase transition
tags: math physics statistical-mechanics
categories: fun
related_posts: false
---

The **Ising model** is the canonical model of a phase transition. Proposed by Wilhelm Lenz in 1920 and solved in 1D by his student Ernst Ising in 1925, it captures the essential physics of ferromagnetism and belongs to a universality class relevant far beyond magnets — from neural networks to protein folding.

### The model

Place binary spins $$s_i = \pm 1$$ on the sites $$i$$ of a lattice. The **Hamiltonian** is

\begin{equation}\label{eq.H}
\mathcal{H} = -J \sum_{\langle ij \rangle} s_i s_j - h \sum_i s_i,
\end{equation}

where $$\langle ij \rangle$$ denotes nearest-neighbour pairs, $$J > 0$$ is the exchange coupling (ferromagnetic), and $$h$$ is an external magnetic field. Parallel spins lower the energy; at low temperature, the system orders.

### Partition function and thermodynamics

The canonical partition function at inverse temperature $$\beta = 1/k_{\rm B}T$$ is

\begin{equation}
Z = \sum_{\{s_i\}} e^{-\beta \mathcal{H}}.
\end{equation}

All thermodynamic quantities follow:

\begin{equation}
F = -k_{\rm B}T \ln Z, \qquad
m = -\frac{\partial F}{\partial h} = \langle s_i \rangle, \qquad
C = -T\frac{\partial^2 F}{\partial T^2}.
\end{equation}

The **order parameter** is the magnetisation per site $$m = \langle s_i \rangle$$. For $$h=0$$, the system has a $$\mathbb{Z}_2$$ symmetry $$s_i \to -s_i$$; a phase transition occurs when this symmetry is spontaneously broken at low $$T$$.

### Exact solution in 1D

In one dimension ($$N$$ spins, periodic boundary conditions), the transfer matrix method gives

\begin{equation}
Z = \lambda_+^N + \lambda_-^N,
\end{equation}

where $$\lambda_\pm = e^{\beta J}\cosh(\beta h) \pm \sqrt{e^{2\beta J}\sinh^2(\beta h) + e^{-2\beta J}}$$.

For $$h = 0$$: $$\lambda_+ = 2\cosh(\beta J)$$, $$\lambda_- = 2\sinh(\beta J)$$, and the correlation length

\begin{equation}
\xi = -\frac{1}{\ln\tanh(\beta J)} \xrightarrow{T\to 0} \tfrac{1}{2} e^{2\beta J}.
\end{equation}

The 1D Ising model has **no phase transition at finite temperature** — the correlation length is always finite for $$T > 0$$. Long-range order is destroyed by a single domain wall costing energy $$2J$$ but gaining entropy $$k_{\rm B} T \ln N$$, so for large $$N$$ the disordered phase always wins.

### Mean-field theory

In the **mean-field approximation**, each spin sees an effective field from its $$z$$ neighbours equal to their average: $$h_{\rm eff} = h + Jz\,m$$. The self-consistency condition is

\begin{equation}\label{eq.mf}
m = \tanh\!\left(\beta(h + Jzm)\right).
\end{equation}

For $$h = 0$$, a non-trivial solution $$m \neq 0$$ exists when the slope of the right-hand side at $$m = 0$$ exceeds 1:

\begin{equation}
\beta J z > 1 \quad \Longrightarrow \quad T < T_c^{\rm MF} = \frac{Jz}{k_{\rm B}}.
\end{equation}

Near $$T_c$$ we expand \eqref{eq.mf} to find

\begin{equation}\label{eq.mfm}
m \approx \pm\sqrt{3}\left(1 - \frac{T}{T_c}\right)^{1/2},
\end{equation}

the order parameter grows as $$(T_c - T)^\beta$$ with **mean-field exponent** $$\beta = 1/2$$.

### Critical exponents and universality

Near a second-order phase transition, thermodynamic quantities diverge as power laws in the reduced temperature $$t = (T - T_c)/T_c$$:

| Quantity | Behaviour | Exponent | MF | 2D Ising |
|---|---|---|---|---|
| Magnetisation | $$m \sim (-t)^\beta$$ | $$\beta$$ | $$1/2$$ | $$1/8$$ |
| Susceptibility | $$\chi \sim \|t\|^{-\gamma}$$ | $$\gamma$$ | $$1$$ | $$7/4$$ |
| Specific heat | $$C \sim \|t\|^{-\alpha}$$ | $$\alpha$$ | $$0$$ (disc.) | $$0$$ (log) |
| Correlation length | $$\xi \sim \|t\|^{-\nu}$$ | $$\nu$$ | $$1/2$$ | $$1$$ |

These exponents are **universal**: they depend only on the dimensionality and symmetry of the order parameter, not on microscopic details (the coupling $$J$$, lattice structure, etc.). This is the content of the **universality hypothesis**, underpinned by the renormalization group.

### Exact solution in 2D

Lars Onsager solved the 2D Ising model exactly in 1944, one of the great triumphs of theoretical physics. For the square lattice with $$h = 0$$:

\begin{equation}
T_c = \frac{2J}{k_{\rm B} \ln(1 + \sqrt{2})} \approx \frac{2.269\, J}{k_{\rm B}},
\end{equation}

and the spontaneous magnetisation for $$T < T_c$$:

\begin{equation}
m(T) = \left[1 - \sinh^{-4}\!\left(\frac{2J}{k_{\rm B} T}\right)\right]^{1/8}.
\end{equation}

The exponent $$1/8$$ is exact and differs dramatically from the mean-field prediction $$1/2$$, illustrating the failure of mean-field theory in low dimensions where fluctuations are strong. The 3D Ising model has no known exact solution; numerical results give $$\beta \approx 0.3265$$.

### Metropolis Monte Carlo

The Ising model is readily simulated by the **Metropolis algorithm**: propose a spin flip $$s_i \to -s_i$$; accept with probability $$\min(1, e^{-\beta \Delta E})$$.

```python
import numpy as np
import matplotlib.pyplot as plt

def ising_step(s, beta, J=1.0):
    N = s.shape[0]
    i, j = np.random.randint(0, N, 2)
    dE = 2 * J * s[i, j] * (
        s[(i+1) % N, j] + s[(i-1) % N, j] +
        s[i, (j+1) % N] + s[i, (j-1) % N]
    )
    if dE < 0 or np.random.rand() < np.exp(-beta * dE):
        s[i, j] *= -1

N = 64
temps = np.linspace(1.5, 3.5, 20)
mag = []
for T in temps:
    s = np.random.choice([-1, 1], size=(N, N))
    beta = 1.0 / T
    for _ in range(500 * N * N):   # thermalise
        ising_step(s, beta)
    m = abs(np.mean(s))
    for _ in range(200 * N * N):   # measure
        ising_step(s, beta)
        m += abs(np.mean(s))
    mag.append(m / (201 * N * N))  # normalise

Tc = 2 / np.log(1 + np.sqrt(2))
plt.axvline(Tc, ls='--', color='gray', label=r'$T_c$ (exact)')
plt.plot(temps, mag, 'o-')
plt.xlabel(r'$T$ (units of $J/k_{\rm B}$)')
plt.ylabel(r'$\langle |m| \rangle$')
plt.legend(); plt.tight_layout(); plt.show()
```

The simulation clearly shows the order–disorder transition at $$T_c \approx 2.269$$: the magnetisation drops abruptly from near 1 to near 0, with the transition region broadening for finite lattices (finite-size scaling).
