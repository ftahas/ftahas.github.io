---
layout: page
title: Black Holes
date: 2026-01-14 11:00:00-0400
description: Event horizons, Hawking radiation, black hole thermodynamics, and the information paradox
tags: physics relativity quantum-mechanics
categories: fun
related_posts: false
---

A **black hole** is a region of spacetime from which nothing — not even light — can escape. Predicted by general relativity and confirmed observationally (gravitational waves 2015, Event Horizon Telescope image of M87* 2019), black holes are also the arena of the deepest unsolved problem in theoretical physics: the **information paradox**.

### The event horizon

The Schwarzschild metric for a mass $$M$$ (see the GR post) is

\begin{equation}
ds^2 = -\!\left(1 - \frac{r_s}{r}\right)c^2 dt^2 + \left(1 - \frac{r_s}{r}\right)^{-1} dr^2 + r^2\,d\Omega^2,
\end{equation}

with $$r_s = 2GM/c^2$$. The surface $$r = r_s$$ is the **event horizon**: the null surface ($$ds^2 = 0$$ with $$dr/dt = c(1 - r_s/r)$$) that separates the region from which causal escape is possible from the region where it is not.

The Schwarzschild coordinates break down at $$r = r_s$$, but in Kruskal–Szekeres coordinates the manifold is smooth there. An infalling observer crosses the horizon without noticing anything special locally (tidal forces are small for large $$M$$). A distant observer, however, sees the infaller **asymptotically freeze** at the horizon and become infinitely redshifted — they never see the crossing.

### Penrose diagrams

A **Penrose (conformal) diagram** compactifies all of spacetime onto a finite diagram, with light rays at $$\pm 45°$$. The maximally extended Schwarzschild solution (the **Kruskal extension**) contains:
- Two exterior regions (two asymptotically flat universes)
- A future singularity ($$r = 0$$, spacelike)
- A past singularity (the "white hole")

The event horizon is the boundary of the causal past of future null infinity $$\mathcal{I}^+$$.

### Rotating black holes: the Kerr metric

A rotating black hole of mass $$M$$ and angular momentum $$J = Mac$$ is described by the **Kerr metric** (1963):

\begin{equation}
ds^2 = -\left(1 - \frac{r_s r}{\Sigma}\right)c^2 dt^2
       - \frac{2r_s r a \sin^2\!\theta}{\Sigma}\,c\,dt\,d\phi
       + \frac{\Sigma}{\Delta}dr^2 + \Sigma\,d\theta^2
       + \left(r^2 + a^2 + \frac{r_s r a^2 \sin^2\!\theta}{\Sigma}\right)\sin^2\!\theta\,d\phi^2,
\end{equation}

where $$a = J/Mc$$, $$\Sigma = r^2 + a^2\cos^2\!\theta$$, $$\Delta = r^2 - r_s r + a^2$$. There are now two horizons (outer and inner) at $$r_\pm = \frac{1}{2}(r_s \pm \sqrt{r_s^2 - 4a^2})$$ and an **ergosphere** outside the outer horizon where no observer can remain stationary. The **Penrose process** extracts rotational energy from the ergosphere, reducing $$J$$.

### Hawking radiation

In 1974, Hawking showed that when quantum field theory is applied near the event horizon, a black hole **radiates thermally** at the **Hawking temperature**:

\begin{equation}\label{eq.TH}
T_H = \frac{\hbar c^3}{8\pi G M k_{\rm B}} \approx \frac{6\times10^{-8}\,{\rm K}}{M/M_\odot}.
\end{equation}

The physical picture: near the horizon, quantum vacuum fluctuations produce virtual particle–antiparticle pairs. Occasionally one partner falls in while the other escapes — the escaping particle carries real energy, which must come at the expense of the black hole's mass.

The radiation is a **perfect black body spectrum** with temperature \eqref{eq.TH}. For stellar-mass black holes $$T_H \sim 10^{-8}$$ K — utterly negligible. For primordial micro-black holes ($$M \sim 10^{15}$$ g), $$T_H \sim 10^{11}$$ K — hot enough to be astrophysically significant.

### Black hole thermodynamics

The four **laws of black hole mechanics** (Bardeen, Carter, Hawking 1973) map exactly onto the laws of thermodynamics:

| Law | Thermodynamics | Black holes |
|---|---|---|
| 0th | $$T$$ uniform at equilibrium | $$\kappa$$ (surface gravity) uniform on horizon |
| 1st | $$dE = T\,dS + \ldots$$ | $$dM = \frac{\kappa}{8\pi G}dA + \Omega\,dJ + \Phi\,dQ$$ |
| 2nd | $$dS \geq 0$$ | $$dA \geq 0$$ (Hawking area theorem) |
| 3rd | $$T \to 0$$ unattainable | $$\kappa \to 0$$ unattainable |

The **Bekenstein–Hawking entropy** is

\begin{equation}\label{eq.SBH}
S_{\rm BH} = \frac{k_{\rm B} c^3}{4G\hbar} A = \frac{k_{\rm B}}{4} \frac{A}{\ell_P^2},
\end{equation}

where $$A = 4\pi r_s^2$$ is the horizon area and $$\ell_P = \sqrt{G\hbar/c^3} \approx 1.6\times10^{-35}$$ m is the **Planck length**. The entropy scales as **area**, not volume — this is the origin of the **holographic principle**.

### The information paradox

Hawking radiation appears to be exactly thermal (mixed state), carrying no information about what fell into the black hole. If the black hole evaporates completely, the information encoded in the initial pure state seems to be lost — violating **unitarity** of quantum mechanics.

This is the **Hawking information paradox** (1976). The current consensus (post-2019 "island formula" developments) is that unitarity is preserved:

\begin{equation}
S_{\rm rad}(t) \leq S_{\rm BH,\,initial},
\end{equation}

following the **Page curve**: the entanglement entropy of the radiation first increases, then decreases back to zero as the black hole evaporates. The mechanism involves **replica wormholes** and **quantum extremal surfaces** contributing to the gravitational path integral — but the full microscopic picture remains an open problem.

The resolution likely requires a quantum theory of gravity, pointing toward string theory or loop quantum gravity. The black hole information paradox is arguably the sharpest clash between general relativity and quantum mechanics we have.
