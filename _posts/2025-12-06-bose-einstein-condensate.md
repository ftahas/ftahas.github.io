---
layout: page
title: Bose–Einstein Condensation
date: 2025-12-06 11:00:00-0400
description: Quantum statistics, the condensation transition, the order parameter, and superfluidity
tags: physics quantum-mechanics statistical-mechanics
categories: fun
related_posts: false
---

**Bose–Einstein condensation** (BEC) is the macroscopic occupation of a single quantum state — a purely quantum phenomenon with no classical analogue. Predicted by Einstein in 1925 (building on Bose's photon statistics), first observed in dilute atomic gases in 1995 (Cornell, Wieman, Ketterle — Nobel Prize 2001).

### Quantum statistics: bosons and fermions

Quantum particles are indistinguishable. Under the exchange of two identical particles, the many-body wavefunction acquires a factor $$e^{i\alpha}$$. Physical states require $$e^{2i\alpha} = 1$$, so $$e^{i\alpha} = \pm 1$$:

- **Bosons** ($$+1$$): integer spin; wavefunctions symmetric under exchange
- **Fermions** ($$-1$$): half-integer spin; wavefunctions antisymmetric (Pauli exclusion)

The mean occupation of a single-particle state with energy $$\epsilon_k$$ in thermal equilibrium is

\begin{equation}
\langle n_k \rangle = \frac{1}{e^{(\epsilon_k - \mu)/k_{\rm B}T} - 1} \quad \text{(Bose–Einstein)},
\end{equation}

where $$\mu \leq \epsilon_{\min}$$ is the chemical potential. As $$\mu \to \epsilon_0^-$$ (the ground-state energy), $$\langle n_0 \rangle \to \infty$$ — bosons can pile up without limit in the ground state.

### The condensation transition

For a non-interacting ideal Bose gas of $$N$$ particles in volume $$V$$, the **condensation temperature** is found by requiring all excited states to saturate at their maximum occupation:

\begin{equation}\label{eq.Tc}
T_c = \frac{2\pi\hbar^2}{m k_{\rm B}}\left(\frac{n}{\zeta(3/2)}\right)^{2/3},
\end{equation}

where $$n = N/V$$ is the number density, $$m$$ the particle mass, and $$\zeta(3/2) \approx 2.612$$ is the Riemann zeta function. For $$T < T_c$$, a **macroscopic fraction**

\begin{equation}
\frac{N_0}{N} = 1 - \left(\frac{T}{T_c}\right)^{3/2}
\end{equation}

occupies the single-particle ground state. This fraction is the **condensate**.

The condition \eqref{eq.Tc} can be rewritten as $$n\lambda_{\rm dB}^3 \gtrsim 2.612$$, where $$\lambda_{\rm dB} = h/\sqrt{2\pi m k_{\rm B} T}$$ is the **thermal de Broglie wavelength**. BEC occurs when the quantum mechanical wave packets of adjacent atoms overlap.

### The order parameter and spontaneous symmetry breaking

The condensate is described by a **macroscopic wavefunction** (order parameter)

\begin{equation}
\Psi(\mathbf{r}, t) = \sqrt{n_0(\mathbf{r}, t)}\, e^{i\theta(\mathbf{r}, t)},
\end{equation}

where $$n_0 = |\Psi|^2$$ is the condensate density and $$\theta$$ its phase. The appearance of a definite phase $$\theta$$ signals the **spontaneous breaking** of the global $$U(1)$$ symmetry $$\Psi \to \Psi e^{i\alpha}$$. This is the same symmetry breaking that underlies superconductivity.

### Gross–Pitaevskii equation

For a weakly interacting BEC (contact interactions with scattering length $$a_s$$, so $$g = 4\pi\hbar^2 a_s/m$$), the condensate dynamics obey the **Gross–Pitaevskii equation**:

\begin{equation}\label{eq.GP}
i\hbar \frac{\partial\Psi}{\partial t} =
\left(-\frac{\hbar^2\nabla^2}{2m} + V_{\rm ext} + g|\Psi|^2\right)\Psi.
\end{equation}

This is a nonlinear Schrödinger equation. The $$g|\Psi|^2$$ term is the **mean-field interaction**: repulsive ($$a_s > 0$$) interactions stabilise the condensate against collapse; attractive ($$a_s < 0$$) interactions lead to collapse above a critical atom number.

In a harmonic trap $$V_{\rm ext} = \frac{1}{2}m\omega^2 r^2$$, the Thomas–Fermi approximation (neglecting kinetic energy for large $$N$$) gives the inverted-parabola density profile

\begin{equation}
n_0(r) = \frac{\mu - \frac{1}{2}m\omega^2 r^2}{g} \quad (r < R_{\rm TF}),
\end{equation}

with Thomas–Fermi radius $$R_{\rm TF} = \sqrt{2\mu/m\omega^2}$$.

### Superfluidity and quantised vortices

The superfluid velocity field is

\begin{equation}
\mathbf{v}_s = \frac{\hbar}{m}\nabla\theta.
\end{equation}

Since $$\mathbf{v}_s = \nabla(\hbar\theta/m)$$ is a gradient, the flow is **irrotational**: $$\nabla\times\mathbf{v}_s = 0$$ except at singularities. The circulation around any closed loop is quantised:

\begin{equation}
\oint \mathbf{v}_s \cdot d\mathbf{l} = \frac{h}{m} \, n, \quad n \in \mathbb{Z}.
\end{equation}

A single **quantised vortex** carries one quantum of circulation $$h/m$$ and a phase winding of $$2\pi$$ around its core, where $$n_0 = 0$$. An array of vortices on a rotating BEC forms an Abrikosov-like lattice — a direct analogue of type-II superconductors.

### Bogoliubov spectrum

Linearising the GP equation around the uniform condensate $$\Psi_0 = \sqrt{n_0}$$ gives the **Bogoliubov dispersion**:

\begin{equation}
E(k) = \hbar\sqrt{\frac{\hbar^2 k^4}{4m^2} + \frac{gn_0}{m}\, k^2}.
\end{equation}

Two limits:
- **Long wavelengths** ($$k \to 0$$): $$E \approx \hbar c_s k$$ — **phonons** propagating at the sound speed $$c_s = \sqrt{gn_0/m}$$. This linear dispersion is responsible for superfluidity (Landau criterion).
- **Short wavelengths** ($$k \to \infty$$): $$E \approx \hbar^2 k^2/2m$$ — free-particle behaviour.

The crossover occurs at the **healing length** $$\xi = \hbar/\sqrt{2mgn_0}$$, the length scale over which the condensate heals around a vortex core or an impurity.

### Experimental realisation

Cornell and Wieman (Boulder, 1995) achieved BEC in $$^{87}$$Rb at $$T_c \approx 170\,$$nK and $$n \sim 10^{13}$$ cm⁻³ using laser cooling followed by **evaporative cooling** in a magnetic trap. The condensate was identified by the characteristic bimodal momentum distribution: a narrow Thomas–Fermi peak (condensate) above a broad thermal cloud. Today BECs are routine tools for studying superfluidity, quantum simulation, atom interferometry, and analogue gravity.
