---
layout: page
title: General Relativity
date: 2025-10-18 11:00:00-0400
description: The equivalence principle, spacetime curvature, Einstein field equations, and the Schwarzschild solution
tags: math physics relativity
categories: fun
related_posts: false
---

General relativity (GR) is Einstein's theory of gravitation, published in 1915. Its central insight is breathtaking: **gravity is not a force but the curvature of spacetime**. Mass and energy warp the geometry of four-dimensional spacetime; freely falling bodies simply follow the straightest possible paths — geodesics — in that curved geometry.

### The equivalence principle

Einstein's key observation (1907) was the **equivalence principle**: the effects of gravity are locally indistinguishable from those of acceleration. An observer in a sealed box cannot tell, by any local experiment, whether they are in a uniform gravitational field or in an accelerating rocket. This elevates gravity from a force to a geometric property.

**Weak equivalence principle**: inertial mass equals gravitational mass — all bodies fall at the same rate (Galileo's experiment). Tested to $$\sim 10^{-15}$$.

**Strong equivalence principle**: locally (in a small enough region), spacetime looks flat and the laws of special relativity hold.

### Riemannian geometry

Spacetime in GR is a four-dimensional **pseudo-Riemannian manifold** with metric $$g_{\mu\nu}$$. The invariant interval is

\begin{equation}
ds^2 = g_{\mu\nu}(x)\, dx^\mu dx^\nu.
\end{equation}

The metric replaces the Newtonian gravitational potential. From it one constructs:

**Christoffel symbols** (connection coefficients):
\begin{equation}
\Gamma^\lambda_{\mu\nu} = \frac{1}{2}g^{\lambda\sigma}\left(
\partial_\mu g_{\nu\sigma} + \partial_\nu g_{\mu\sigma} - \partial_\sigma g_{\mu\nu}
\right).
\end{equation}

**Riemann curvature tensor**:
\begin{equation}
R^\rho{}_{\sigma\mu\nu} = \partial_\mu\Gamma^\rho_{\nu\sigma} - \partial_\nu\Gamma^\rho_{\mu\sigma}
+ \Gamma^\rho_{\mu\lambda}\Gamma^\lambda_{\nu\sigma} - \Gamma^\rho_{\nu\lambda}\Gamma^\lambda_{\mu\sigma}.
\end{equation}

**Ricci tensor and scalar**:
\begin{equation}
R_{\mu\nu} = R^\lambda{}_{\mu\lambda\nu}, \qquad R = g^{\mu\nu}R_{\mu\nu}.
\end{equation}

**Einstein tensor**:
\begin{equation}
G_{\mu\nu} = R_{\mu\nu} - \tfrac{1}{2}g_{\mu\nu} R.
\end{equation}

The Einstein tensor satisfies $$\nabla^\mu G_{\mu\nu} = 0$$ (Bianchi identity), which ensures conservation of energy-momentum.

### Geodesics

A freely falling particle follows a **geodesic** — the curve that extremises proper time:

\begin{equation}\label{eq.geodesic}
\frac{d^2 x^\mu}{d\tau^2} + \Gamma^\mu_{\alpha\beta}\frac{dx^\alpha}{d\tau}\frac{dx^\beta}{d\tau} = 0.
\end{equation}

The Christoffel symbol terms play the role of the "gravitational force" in the new coordinates. In flat spacetime ($$\Gamma = 0$$) this reduces to $$d^2x^\mu/d\tau^2 = 0$$: uniform motion.

### Einstein field equations

The **Einstein field equations** (EFE) relate spacetime curvature to the energy-momentum content of matter:

\begin{equation}\label{eq.EFE}
\boxed{G_{\mu\nu} + \Lambda g_{\mu\nu} = \frac{8\pi G}{c^4}\, T_{\mu\nu}.}
\end{equation}

Here $$T_{\mu\nu}$$ is the **stress-energy tensor**, $$G = 6.674\times10^{-11}$$ N m² kg⁻² is Newton's constant, and $$\Lambda$$ is the **cosmological constant** (associated with dark energy). The prefactor $$8\pi G/c^4 \approx 2\times 10^{-43}$$ N⁻¹ expresses the extraordinary stiffness of spacetime — enormous energy-momentum is needed to produce a measurable curvature.

Despite their compact appearance, the EFE are ten coupled, nonlinear partial differential equations for $$g_{\mu\nu}$$. Exact solutions exist only in highly symmetric situations.

### The Schwarzschild solution

Karl Schwarzschild found the exact solution for a static, spherically symmetric vacuum ($$T_{\mu\nu} = 0$$, $$\Lambda = 0$$) in 1916 — just weeks after Einstein published the EFE:

\begin{equation}\label{eq.schwarz}
ds^2 = -\!\left(1 - \frac{r_s}{r}\right)c^2 dt^2
      + \left(1 - \frac{r_s}{r}\right)^{-1} dr^2
      + r^2\,d\Omega^2,
\end{equation}

where $$d\Omega^2 = d\theta^2 + \sin^2\theta\, d\phi^2$$ and the **Schwarzschild radius** is

\begin{equation}
r_s = \frac{2GM}{c^2}.
\end{equation}

For the Sun, $$r_s \approx 3$$ km (the Sun's radius is $$\sim 7\times10^5$$ km); for the Earth, $$r_s \approx 9$$ mm. The metric \eqref{eq.schwarz} is singular at $$r = r_s$$ — not a physical singularity, but a **coordinate singularity** (the event horizon). The true singularity lies at $$r = 0$$.

### Predictions confirmed by observation

**1. Perihelion precession of Mercury.** GR predicts an extra 43 arcseconds/century, matching observation precisely — a long-standing discrepancy with Newtonian gravity.

**2. Gravitational deflection of light.** A ray passing the Sun is deflected by $$1.75''$$, twice the Newtonian prediction. Confirmed by Eddington's 1919 solar eclipse expedition.

**3. Gravitational redshift.** A photon climbing out of a gravitational well loses energy:

\begin{equation}
\frac{\Delta\nu}{\nu} = -\frac{GM}{rc^2}.
\end{equation}

Confirmed to high precision by Pound–Rebka (1959) and atomic clocks on GPS satellites (which require GR corrections of $$\sim 45\,\mu$$s/day).

**4. Gravitational waves.** The linearised EFE admit wave solutions that propagate at $$c$$. Detected directly by LIGO in 2015 from a binary black hole merger — 100 years after the EFE.

### The post-Newtonian limit

In the weak-field, slow-motion limit, the EFE reduce to Poisson's equation

\begin{equation}
\nabla^2\Phi = 4\pi G\rho,
\end{equation}

where $$\Phi$$ is the Newtonian gravitational potential and $$g_{00} \approx -(1 + 2\Phi/c^2)$$. Newtonian gravity is thus the leading approximation to GR when both $$v/c \ll 1$$ and $$\Phi/c^2 \ll 1$.

### Cosmology and Friedmann equations

Applying the EFE to a homogeneous, isotropic universe (Friedmann–Lemaître–Robertson–Walker metric) gives the **Friedmann equations**:

\begin{equation}
\left(\frac{\dot{a}}{a}\right)^2 = \frac{8\pi G}{3}\rho + \frac{\Lambda c^2}{3} - \frac{kc^2}{a^2},
\end{equation}

\begin{equation}
\frac{\ddot{a}}{a} = -\frac{4\pi G}{3}\!\left(\rho + \frac{3p}{c^2}\right) + \frac{\Lambda c^2}{3},
\end{equation}

where $$a(t)$$ is the scale factor, $$k = -1, 0, +1$$ is the spatial curvature, and $$p$$ is pressure. The accelerating expansion of the universe ($$\ddot{a} > 0$$), driven by $$\Lambda > 0$$, was discovered in 1998 — one of the deepest open problems in physics today.
