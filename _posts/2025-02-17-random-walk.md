---
layout: page
title: The Random Walk and Diffusion
date: 2025-02-17 11:00:00-0400
description: From coin flips to Brownian motion — the random walk, its diffusion limit, and the central limit theorem
tags: math physics probability
categories: fun
related_posts: false
---

A **random walk** is one of the simplest stochastic processes, yet it underlies Brownian motion, diffusion, finance, and polymer physics. Starting from a single coin flip, we can derive the heat equation itself.

### The 1D random walk

Consider a particle on the integer line. At each discrete time step $$n$$, it moves right (+1) or left (−1) with equal probability $$\frac{1}{2}$$. Define the increments

\begin{equation}
\xi_i = \begin{cases} +1 & \text{with probability } \tfrac{1}{2}, \\ -1 & \text{with probability } \tfrac{1}{2}. \end{cases}
\end{equation}

The position after $$N$$ steps is

\begin{equation}
X_N = \sum_{i=1}^{N} \xi_i.
\end{equation}

Since each $$\xi_i$$ is independent with $$\mathbb{E}[\xi_i]=0$$ and $$\text{Var}(\xi_i)=1$$:

\begin{equation}
\mathbb{E}[X_N] = 0, \qquad \mathbb{E}[X_N^2] = N.
\end{equation}

The **mean square displacement grows linearly** in time — the hallmark of diffusive transport, as opposed to $$\mathbb{E}[X_N^2] \propto N^2$$ for ballistic (constant-velocity) motion.

### Exact distribution

The position $$X_N$$ can be written as $$X_N = 2S_N - N$$ where $$S_N \sim \text{Binomial}(N, \tfrac{1}{2})$$ counts the number of right steps. The probability of being at position $$k$$ (requiring $$(N+k)/2$$ rights, so $$k$$ and $$N$$ have the same parity) is

\begin{equation}
P(X_N = k) = \binom{N}{\frac{N+k}{2}} 2^{-N}.
\end{equation}

### The diffusion limit and the central limit theorem

Let the step size be $$\ell$$ and the time step be $$\tau$$. After time $$t = N\tau$$, the position is $$x = X_N \ell$$. By the **central limit theorem**, for large $$N$$:

\begin{equation}\label{eq.gaussian}
P(x, t) \approx \frac{1}{\sqrt{4\pi D t}}\, \exp\!\left(-\frac{x^2}{4Dt}\right),
\end{equation}

where the **diffusion coefficient** is

\begin{equation}
D = \frac{\ell^2}{2\tau}.
\end{equation}

This Gaussian spreading is the solution to the **diffusion equation** (heat equation):

\begin{equation}\label{eq.diffusion}
\frac{\partial P}{\partial t} = D\, \frac{\partial^2 P}{\partial x^2},
\end{equation}

with initial condition $$P(x,0) = \delta(x)$$. The random walk is, in the continuum limit, precisely Brownian motion.

### Derivation of the diffusion equation from the walk

The Chapman–Kolmogorov relation for the walk gives

\begin{equation}
P(x, t+\tau) = \tfrac{1}{2} P(x-\ell, t) + \tfrac{1}{2} P(x+\ell, t).
\end{equation}

Taylor-expanding each side to leading order in $$\tau$$ and $$\ell^2$$:

\begin{equation}
P + \tau \partial_t P = P + \frac{\ell^2}{2}\partial_{xx} P + O(\ell^4),
\end{equation}

which gives equation \eqref{eq.diffusion} in the limit $$\ell, \tau \to 0$$ with $$D = \ell^2 / 2\tau$$ fixed.

### The 3D random walk and return probability

In $$d$$ dimensions, the mean square displacement after $$N$$ steps of length $$\ell$$ remains $$\langle r^2 \rangle = N\ell^2$$, but the **return probability** changes dramatically with dimension.

**Pólya's theorem** (1921): A simple random walk on $$\mathbb{Z}^d$$ returns to the origin with probability 1 if and only if $$d \leq 2$$. For $$d \geq 3$$ the walk is *transient* — it escapes to infinity almost surely. Explicitly, the return probability in $$d = 3$$ is approximately $$0.3405$$.

### First-passage time

For a 1D walk, the **first-passage time** $$T$$ to reach position $$a > 0$$ starting from the origin has distribution with heavy tail:

\begin{equation}
P(T = n) \sim \frac{a}{\sqrt{4\pi D}} \, n^{-3/2} \quad (n \to \infty).
\end{equation}

This $$n^{-3/2}$$ power law means the expected first-passage time is **infinite** (for an unbiased walk) — a striking illustration that rare events dominate the statistics of diffusive processes.

### Self-avoiding walks and polymers

A **self-avoiding walk** (SAW) forbids the walker from revisiting any site. This seemingly simple modification captures the physics of a polymer in a good solvent. The end-to-end distance scales as

\begin{equation}
\langle r^2 \rangle^{1/2} \sim N^\nu,
\end{equation}

where the **Flory exponent** $$\nu$$ takes the exact value $$\nu = 3/(d+2)$$ in Flory mean-field theory (exact in $$d = 1$$: $$\nu = 1$$; very good in $$d = 2$$: $$\nu = 3/4$$ vs. exact $$\nu = 3/4$$; slightly off in $$d = 3$$: $$\nu \approx 0.588$$ vs. Flory's $$3/5$$). SAWs belong to a different universality class than simple diffusion.

### Simulation

The following Python snippet simulates a 2D random walk and estimates the diffusion coefficient from the mean square displacement:

```python
import numpy as np
import matplotlib.pyplot as plt

rng = np.random.default_rng(42)
N, n_walks = 10_000, 500
steps = rng.choice([-1, 1], size=(n_walks, N, 2))
positions = np.cumsum(steps, axis=1)          # shape (n_walks, N, 2)
msd = np.mean(np.sum(positions**2, axis=2), axis=0)  # mean over walkers

t = np.arange(1, N + 1)
D_est = np.polyfit(t, msd, 1)[0] / 2   # MSD = 2d * D * t, d=2 => factor 4
print(f"Estimated D = {D_est:.4f}  (expected 0.5)")

plt.loglog(t, msd, label='MSD')
plt.loglog(t, 2 * t, '--', label=r'$2dt$')
plt.xlabel('Steps'); plt.ylabel(r'$\langle r^2 \rangle$')
plt.legend(); plt.tight_layout(); plt.show()
```

The log–log plot confirms $$\langle r^2 \rangle \propto t^1$$, the diffusive scaling. Any deviation from slope 1 signals anomalous diffusion — subdiffusive ($$\langle r^2 \rangle \propto t^\alpha$$, $$\alpha < 1$$) in crowded environments, or superdiffusive ($$\alpha > 1$$) in Lévy flights.
