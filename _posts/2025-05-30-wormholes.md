---
layout: page
title: Wormholes
date: 2025-05-30 11:00:00-0400
description: Einstein–Rosen bridges, Morris–Thorne wormholes, exotic matter, and traversability
tags: physics relativity
categories: fun
related_posts: false
---

A **wormhole** (or Einstein–Rosen bridge) is a hypothetical tunnel connecting two separate regions of spacetime. They arise as exact solutions of Einstein's field equations, but their physical realisability requires matter with exotic properties — and they sit at the intersection of classical general relativity, quantum field theory, and quantum gravity.

### The Einstein–Rosen bridge

In 1935, Einstein and Rosen noticed that the maximally extended Schwarzschild solution contains **two** exterior regions connected by a throat — the Einstein–Rosen bridge. In Kruskal–Szekeres coordinates $$(T, X)$$:

\begin{equation}
ds^2 = \frac{32G^3M^3}{r}\,e^{-r/2GM}\left(-dT^2 + dX^2\right) + r^2\,d\Omega^2,
\end{equation}

where $$r$$ is defined implicitly by $$T^2 - X^2 = (1 - r/2GM)e^{r/2GM}$$. The two exterior regions ($$|X| > |T|$$) are connected at $$T = 0$$ by a minimal 2-sphere of radius $$r = r_s$$. The trouble: this bridge is **non-traversable**. It pinches off (collapses to $$r = 0$$) faster than any signal can cross it, even at the speed of light. One cannot travel through a Schwarzschild wormhole.

### Morris–Thorne traversable wormholes

In 1988, Morris and Thorne asked: what metric would describe a traversable wormhole, and what matter would it require? They wrote the general static, spherically symmetric wormhole metric:

\begin{equation}\label{eq.MT}
ds^2 = -e^{2\Phi(r)}c^2\,dt^2 + \frac{dr^2}{1 - b(r)/r} + r^2\,d\Omega^2,
\end{equation}

where $$\Phi(r)$$ is the **redshift function** and $$b(r)$$ is the **shape function**. Traversability requires:

1. **No event horizon**: $$e^{2\Phi}$$ is finite and non-zero everywhere (no infinite redshift).
2. **Flaring-out condition**: the throat at $$r = r_0$$ (where $$b(r_0) = r_0$$) must satisfy $$b'(r_0) < 1$$, equivalently $$b'(r_0) \leq 1$$.
3. **Asymptotic flatness**: $$\Phi \to 0$$ and $$b/r \to 0$$ as $$r \to \infty$$.

Plugging \eqref{eq.MT} into the Einstein field equations, the flaring-out condition requires the **null energy condition (NEC) to be violated** at the throat:

\begin{equation}
T_{\mu\nu}k^\mu k^\nu < 0 \quad \text{for some null vector } k^\mu.
\end{equation}

This means: the matter threading the wormhole throat must have **negative energy density** (as measured by null observers) — so-called **exotic matter**.

### Exotic matter and the Casimir effect

Classical matter satisfies the NEC; quantum fields need not. The **Casimir effect** — a measurable attractive force between parallel conducting plates due to the modification of the vacuum fluctuation spectrum — produces a region of negative energy density between the plates:

\begin{equation}
\rho_{\rm Casimir} = -\frac{\pi^2 \hbar c}{240\, d^4},
\end{equation}

where $$d$$ is the plate separation. This is real, measured negative energy. Whether it can be concentrated and sustained on the scale needed to stabilise a macroscopic wormhole remains an open question — and current estimates suggest the amount of exotic matter needed is enormous, perhaps comparable to the mass of Jupiter.

**Quantum inequalities** (Ford, Roman) constrain how negative energy can be: the more negative the energy, the shorter the time interval over which it can persist. These constraints severely restrict the geometry of traversable wormholes.

### Interstellar travel and time machines

A traversable wormhole could, in principle, allow **faster-than-light travel** between distant points: if both mouths are in asymptotically flat space, the proper distance through the tunnel can be much shorter than the spatial distance around it.

More dramatically, if one mouth is accelerated (or placed in a gravitational field), the two mouths' clocks desynchronise. Bringing the mouths close together then creates a **closed timelike curve** — a time machine. This led Hawking to propose the **Chronology Protection Conjecture**: quantum effects (back-reaction of Casimir-like negative energy) always destabilise wormholes before closed timelike curves can form. A full quantum gravity treatment is needed to settle this.

### Lorentzian vs. Euclidean wormholes

In Euclidean (imaginary time, $$t \to -i\tau$$) quantum gravity, wormhole configurations appear naturally in the path integral and contribute to correlators between distant spacetime regions. These **Euclidean wormholes** are non-traversable (they connect different Euclidean time slices) but are thought to play a role in:

- Inducing non-perturbative global symmetry violations
- The **baby universe** formulation of quantum cosmology (Coleman 1988)
- The **island formula** for black hole entropy and the Page curve (2019): replica wormholes saddle-point contributions resolve the information paradox

### The ER = EPR connection

Maldacena and Susskind (2013) conjectured that the Einstein–Rosen bridge connecting two entangled black holes and the Einstein–Podolsky–Rosen entanglement of the same black holes are **the same phenomenon** — a deep identification between geometry and entanglement (see the ER = EPR post). In this picture, any two entangled particles are connected by a microscopic, non-traversable wormhole. Traversability requires a sufficient amount of entanglement — and negative energy — to hold the throat open, linking quantum information theory and spacetime geometry at the deepest level.
