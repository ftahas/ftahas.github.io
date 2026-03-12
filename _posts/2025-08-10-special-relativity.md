---
layout: page
title: Special Relativity and the Covariant Form of Maxwell's Equations
date: 2025-08-10 11:00:00-0400
description: Lorentz transformations, four-vectors, the electromagnetic field tensor, and how Maxwell's equations unify into two covariant equations
tags: math physics electromagnetism relativity
categories: fun
related_posts: false
---

Einstein's special relativity (1905) was, in a deep sense, already implicit in Maxwell's equations of electromagnetism (1865). The requirement that the speed of light $$c$$ be the same in all inertial frames forces a revision of classical kinematics — and, in return, reveals that the six components of **E** and **B** are simply different aspects of a single antisymmetric tensor.

### Postulates and the Lorentz transformation

**Two postulates** underlie special relativity:

1. The laws of physics are the same in all inertial frames.
2. The speed of light in vacuum is $$c$$ in all inertial frames.

These force the **Lorentz transformation** between frames $$S$$ and $$S'$$ (moving at velocity $$v$$ along $$x$$):

\begin{equation}\label{eq.lorentz}
t' = \gamma\!\left(t - \frac{vx}{c^2}\right), \quad
x' = \gamma(x - vt), \quad y' = y, \quad z' = z,
\end{equation}

with the **Lorentz factor** $$\gamma = (1 - v^2/c^2)^{-1/2}$$. The key consequences are **time dilation** ($$\Delta t' = \gamma\,\Delta t_0$$) and **length contraction** ($$\Delta x' = \Delta x_0/\gamma$$).

### Spacetime and four-vectors

Minkowski (1907) realised the correct arena is **spacetime** $$\mathbb{R}^{1,3}$$ with the metric

\begin{equation}\label{eq.metric}
ds^2 = -c^2 dt^2 + dx^2 + dy^2 + dz^2 = \eta_{\mu\nu}\, dx^\mu dx^\nu,
\end{equation}

where $$\eta_{\mu\nu} = \text{diag}(-1,+1,+1,+1)$$ is the **Minkowski metric** (using the $$(-+++)$$ signature). Greek indices run $$0,1,2,3$$.

The **four-position** is $$x^\mu = (ct, x, y, z)$$. The Lorentz transformation \eqref{eq.lorentz} is a linear map $$x'^\mu = \Lambda^\mu{}_\nu x^\nu$$ that preserves $$\eta_{\mu\nu}$$:

\begin{equation}
\Lambda^\alpha{}_\mu \,\eta_{\alpha\beta}\, \Lambda^\beta{}_\nu = \eta_{\mu\nu}.
\end{equation}

Any set of four quantities transforming the same way as $$x^\mu$$ is a **four-vector**. Key examples:

\begin{equation}
p^\mu = (E/c,\, \mathbf{p}), \quad
j^\mu = (c\rho,\, \mathbf{J}), \quad
A^\mu = (\phi/c,\, \mathbf{A}),
\end{equation}

where $$p^\mu$$ is the four-momentum, $$j^\mu$$ the four-current, and $$A^\mu$$ the four-potential.

The invariant $$p_\mu p^\mu = -m^2c^2$$ gives the **energy-momentum relation**:

\begin{equation}
\boxed{E^2 = (pc)^2 + (mc^2)^2.}
\end{equation}

### The electromagnetic field tensor

The electric and magnetic fields are encoded in the **antisymmetric field-strength tensor**

\begin{equation}\label{eq.F}
F_{\mu\nu} = \partial_\mu A_\nu - \partial_\nu A_\mu,
\end{equation}

where $$\partial_\mu = (\partial_t/c, \nabla)$$. In matrix form:

\begin{equation}
F^{\mu\nu} = \begin{pmatrix}
0 & -E_x/c & -E_y/c & -E_z/c \\
E_x/c & 0 & -B_z & B_y \\
E_y/c & B_z & 0 & -B_x \\
E_z/c & -B_y & B_x & 0
\end{pmatrix}.
\end{equation}

Under a Lorentz boost along $$x$$ with velocity $$v$$, the components mix:

\begin{equation}
E'_x = E_x, \quad
E'_y = \gamma(E_y - vB_z), \quad
E'_z = \gamma(E_z + vB_y),
\end{equation}
\begin{equation}
B'_x = B_x, \quad
B'_y = \gamma\!\left(B_y + \frac{v}{c^2}E_z\right), \quad
B'_z = \gamma\!\left(B_z - \frac{v}{c^2}E_y\right).
\end{equation}

A purely electric field in one frame has a magnetic component in another — **E** and **B** are not independently Lorentz-covariant. They are two faces of $$F_{\mu\nu}$$.

### Maxwell's equations in covariant form

Maxwell's four equations reduce to **two** in covariant notation.

**The inhomogeneous equations** (Gauss's law + Ampère's law) become

\begin{equation}\label{eq.inh}
\boxed{\partial_\nu F^{\mu\nu} = \mu_0 j^\mu.}
\end{equation}

**The homogeneous equations** (Gauss's law for magnetism + Faraday's law) follow automatically from the definition \eqref{eq.F} via the Bianchi identity:

\begin{equation}\label{eq.hom}
\boxed{\partial_{[\lambda} F_{\mu\nu]} = 0,}
\end{equation}

or equivalently $$\partial_\lambda F_{\mu\nu} + \partial_\mu F_{\nu\lambda} + \partial_\nu F_{\lambda\mu} = 0$$.

Equation \eqref{eq.inh} encodes:
- $$\mu = 0$$: $$\nabla \cdot \mathbf{E} = \rho/\epsilon_0$$ (Gauss)
- $$\mu = i$$: $$\nabla \times \mathbf{B} - \dot{\mathbf{E}}/c^2 = \mu_0 \mathbf{J}$$ (Ampère-Maxwell)

Equation \eqref{eq.hom} encodes:
- $$\lambda\mu\nu = 123$$: $$\nabla \cdot \mathbf{B} = 0$$
- other components: $$\nabla \times \mathbf{E} + \dot{\mathbf{B}} = 0$$ (Faraday)

In the covariant form, the invariance of Maxwell's equations under Lorentz transformations is manifest: both sides of \eqref{eq.inh} are four-tensors, so the equation holds in all inertial frames.

### The two Lorentz invariants

From $$F_{\mu\nu}$$ one can form two independent Lorentz scalars:

\begin{equation}
\mathcal{F} = \tfrac{1}{2}F_{\mu\nu}F^{\mu\nu} = B^2 - E^2/c^2,
\end{equation}
\begin{equation}
\mathcal{G} = \tfrac{1}{4}F_{\mu\nu}\tilde{F}^{\mu\nu} = \mathbf{E}\cdot\mathbf{B}/c,
\end{equation}

where $$\tilde{F}^{\mu\nu} = \frac{1}{2}\epsilon^{\mu\nu\rho\sigma}F_{\rho\sigma}$$ is the dual tensor. These are the only independent invariants of the electromagnetic field.

### The Lorentz force and equations of motion

The four-force on a charged particle is

\begin{equation}
\frac{dp^\mu}{d\tau} = q F^{\mu\nu} u_\nu,
\end{equation}

where $$u^\mu = dx^\mu/d\tau = \gamma(c, \mathbf{v})$$ is the four-velocity. The spatial components reproduce the Lorentz force law $$\mathbf{F} = q(\mathbf{E} + \mathbf{v}\times\mathbf{B})$$; the time component gives the power $$dE/dt = q\mathbf{E}\cdot\mathbf{v}$$.

### From Maxwell to photons

The wave equation follows from \eqref{eq.inh} in vacuum ($$j^\mu = 0$$) in Lorenz gauge ($$\partial_\mu A^\mu = 0$$):

\begin{equation}
\Box A^\mu = 0, \quad \Box \equiv \partial_\mu \partial^\mu = -\frac{1}{c^2}\partial_t^2 + \nabla^2.
\end{equation}

Plane-wave solutions $$A^\mu \propto e^{ik_\nu x^\nu}$$ require $$k_\mu k^\mu = 0$$, i.e. $$\omega = c|\mathbf{k}|$$ — the dispersion relation of **massless photons**. The masslessness of the photon is equivalent to gauge invariance of $$A^\mu$$, which is equivalent to the homogeneous equation \eqref{eq.hom}. Special relativity, electromagnetism, and quantum field theory are deeply intertwined from the very start.
