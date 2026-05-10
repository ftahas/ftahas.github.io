---
layout: page
title: Quantum theory of scattering by a central potential
date: 2026-05-10 00:00:00-0000
description: A complete d-dimensional treatment of quantum scattering by a central potential — from hyperspherical harmonics and Bessel functions to phase shifts, cross sections, and specific potentials
img:
tags: math physics quantum
categories: fun
related_posts: false
---

These notes develop the complete theory of quantum scattering by a central potential
$$V(\mathbf{r}) = V(r)$$ in $$d$$ spatial dimensions. The treatment is self-contained: we
derive hyperspherical harmonics from scratch, reduce the radial equation to a Bessel
equation, establish the scattering boundary condition from first principles, and apply
the resulting partial-wave formalism to several concrete potentials. The full notes are
available [here](/assets/pdf/Quantum_scattering_d_dim.pdf).

---

### 1 Notation and Conventions

Throughout, $$d$$ denotes the number of spatial dimensions. The fundamental parameter is

\begin{equation}\label{eq.nu}
\nu \equiv \frac{d-2}{2},
\end{equation}

so that $$\nu = \tfrac{1}{2}$$ for $$d = 3$$. A closely related quantity, the **effective
angular momentum**, is

\begin{equation}\label{eq.lambda.def}
\lambda \equiv \ell + \nu = \ell + \frac{d-2}{2}.
\end{equation}

The surface area of the unit sphere $$S^{d-1} \subset \mathbb{R}^d$$ is

\begin{equation}\label{eq.Omega.d}
\Omega_d = \frac{2\pi^{d/2}}{\Gamma(d/2)}.
\end{equation}

To derive this, factor the Gaussian integral in $$d$$ dimensions as a radial integral
times the solid angle:

$$
\pi^{d/2} = \int_{\mathbb{R}^d} \mathrm{e}^{-r^2}\,\mathrm{d}^d r = \Omega_d \int_0^\infty r^{d-1}\mathrm{e}^{-r^2}\mathrm{d}r = \frac{\Omega_d}{2}\,\Gamma(d/2),
$$

using $$t = r^2$$ in the radial integral, which isolates $$\Omega_d$$.

We single out $$\theta \equiv \theta_1 \in [0,\pi]$$ as the **scattering angle** (the angle
between $$\hat{\mathbf{r}}$$ and the beam axis $$\hat{\mathbf{e}}_d$$). For any axially
symmetric function $$g(\theta)$$, the full angular integral reduces to

$$
\int_{S^{d-1}} g(\theta)\,\mathrm{d}\Omega_{d-1} = \omega_{d-1}\int_0^\pi g(\theta)\sin^{d-2}\theta\,\mathrm{d}\theta = \omega_{d-1}\int_{-1}^{1} g(x)(1-x^2)^{\nu-1/2}\mathrm{d}x,
$$

where $$x = \cos\theta$$ and the transverse solid angle is
$$\omega_{d-1} = \Omega_{d-1} = 2\pi^{(d-1)/2}/\Gamma((d-1)/2)$$.

---

## Part I — The Universal Framework

The whole content of this part is independent of the choice of potential $$V(r)$$. We
construct the framework once; in Part II we apply it to specific potentials.

---

### 2 Conditions on the Potential

Before assembling the framework, we state the conditions that $$V(r)$$ must satisfy.
The principal one is the **short-range condition**, which underpins the entire
construction.

#### 2.1 The short-range condition

A central potential $$V(r)$$ is **short-range** if

\begin{equation}\label{eq.short.range}
\lim_{r\to\infty} r\,V(r) = 0.
\end{equation}

Equivalently, $$V(r)$$ decays faster than $$1/r$$ at infinity: $$V(r) = o(1/r)$$ as
$$r\to\infty$$. Examples: $$V \propto \mathrm{e}^{-\mu r}/r$$ (Yukawa), $$V \propto 1/r^n$$
with $$n \geq 2$$, any compactly supported $$V$$, any Gaussian. The counter-example is the
Coulomb potential itself, $$V \propto 1/r$$, for which $$rV(r) = \text{const} \neq 0$$.

#### 2.2 Why the short-range condition is essential

The condition enters at three crucial points of the framework.

First, in the **asymptotic boundary condition**:

$$
\psi(\mathbf{r}) \xrightarrow{r\to\infty} \mathrm{e}^{ikz} + f(\theta)\,\frac{\mathrm{e}^{ikr}}{r^{(d-1)/2}},
$$

which presupposes that, at large $$r$$, the particle is effectively free — moving as a
plane wave plus outgoing spherical waves. This requires $$V$$ to become negligible at
large distances sufficiently fast not to distort the asymptotic phase.

Second, in the **existence of phase shifts via matching**: the phase shifts $$\delta_\ell$$
are defined by matching the interior solution (with $$V$$) with the free solutions
$$J_\lambda, N_\lambda$$ in an exterior region where $$V \approx 0$$. This matching only
makes sense if there is some $$R_0$$ beyond which $$V$$ is negligible.

Third, in the **convergence of the partial-wave sum**: the expansion
$$f(\theta) = \sum_\ell(\ldots) e^{i\delta_\ell}\sin\delta_\ell C_\ell^\nu(\cos\theta)$$
converges pointwise because the threshold behaviour $$\delta_\ell \sim k^{2\ell+d-2}$$
suppresses the contributions of large $$\ell$$. This threshold behaviour depends on the
short-range condition.

The three points above all fail for the Coulomb potential: the asymptotic wave function
acquires a logarithmic phase $$e^{i\eta\ln(2kr)}$$ that never disappears; the matching
with free Bessel functions fails; and the partial-wave sum diverges. Coulomb scattering
is a qualitatively distinct problem, treated in Section 12.

#### 2.3 The critical line: why exactly $$1/r$$?

The power $$1/r$$ is the limiting case — the exact boundary between short- and long-range
behaviour. To see this, consider $$V(r) \sim C/r^n$$ at large $$r$$. The phase accumulated
by the wave function between $$R$$ and $$\infty$$ is

$$
\Delta\phi \sim \int_R^\infty \left[\sqrt{k^2 - U(r)} - k\right]\mathrm{d}r \approx -\frac{1}{2k}\int_R^\infty U(r)\,\mathrm{d}r \propto \int_R^\infty \frac{1}{r^n}\,\mathrm{d}r.
$$

This integral converges for $$n > 1$$ (short range: a finite phase correction) and diverges
for $$n \leq 1$$ (long range: an infinite phase at infinity). The case $$n = 1$$ diverges
logarithmically, which is exactly the logarithmic phase $$\eta\ln(2kr)$$ found in the
Coulomb case.

#### 2.4 Other conditions and summary

For completeness, we also require: (i) that $$V(r)$$ be real, which guarantees $$\hat{H}$$
Hermitian and the $$S$$-matrix unitary; (ii) that it be regular at the origin
($$r^2 V(r) \to 0$$), guaranteeing that the centrifugal barrier $$(\lambda^2 - \tfrac{1}{4})/r^2$$
dominates near the origin; and (iii) that it be locally integrable,
$$\int_0^{R_0} r^{d-1}|V(r)|\,\mathrm{d}r < \infty$$.

In summary, throughout the document, $$V(r)$$ is assumed real, spherically symmetric
(central), locally integrable, regular at the origin, and above all **short-range**:
$$rV(r)\to 0$$ as $$r\to\infty$$. The short-range condition is the most restrictive and
is the one whose failure (for the Coulomb potential) forces a separate treatment.

---

### 3 Hyperspherical Coordinates and the Laplacian

#### 3.1 Definition of the coordinate system

A point $$\mathbf{r} = (x_1,\ldots,x_d)\in\mathbb{R}^d$$ is parametrised by a radial
coordinate $$r \geq 0$$ and $$d-1$$ angles $$(\theta_1,\theta_2,\ldots,\theta_{d-2},\varphi)$$
via

\begin{equation}\label{eq.hypersph.coord}
\begin{aligned}
x_1 &= r\sin\theta_1\sin\theta_2\cdots\sin\theta_{d-2}\cos\varphi,\\
x_2 &= r\sin\theta_1\sin\theta_2\cdots\sin\theta_{d-2}\sin\varphi,\\
x_k &= r\sin\theta_1\sin\theta_2\cdots\sin\theta_{d-k}\cos\theta_{d-k+1}, \quad 3 \leq k \leq d-1,\\
x_d &= r\cos\theta_1,
\end{aligned}
\end{equation}

with $$r\geq 0$$, $$\theta_j \in [0,\pi]$$ for $$j=1,\ldots,d-2$$, and $$\varphi\in[0,2\pi)$$.
The Jacobian of the transformation is

$$
J = r^{d-1}\prod_{j=1}^{d-2}\sin^{d-1-j}\theta_j,
$$

verifiable by induction in $$d$$. The volume element is therefore

$$
\mathrm{d}^d r = r^{d-1}\,\mathrm{d}r\,\mathrm{d}\Omega_d, \qquad \mathrm{d}\Omega_d = \prod_{j=1}^{d-2}\sin^{d-1-j}\theta_j\,\mathrm{d}\theta_j\,\mathrm{d}\varphi.
$$

#### 3.2 The Laplacian in hyperspherical coordinates

In any orthogonal curvilinear coordinate system, the Laplacian splits into a radial part
and an angular part. In $$d$$-dimensional hyperspherical coordinates,

\begin{equation}\label{eq.laplacian.d}
\nabla_d^2 = \frac{1}{r^{d-1}}\frac{\partial}{\partial r}\!\left(r^{d-1}\frac{\partial}{\partial r}\right) + \frac{1}{r^2}\,\hat{\Delta}_d,
\end{equation}

where $$\hat{\Delta}_d$$ is a purely angular operator on $$S^{d-1}$$ (the
Laplace–Beltrami operator on the sphere). The radial part can be rewritten as

$$
\frac{1}{r^{d-1}}\frac{\partial}{\partial r}\!\left(r^{d-1}\frac{\partial}{\partial r}\right) = \frac{\partial^2}{\partial r^2} + \frac{d-1}{r}\frac{\partial}{\partial r}.
$$

#### 3.3 The angular operator $$\hat{\Delta}_d$$

The operator $$\hat{\Delta}_d$$ acts on functions on $$S^{d-1}$$ and can be defined
recursively. Writing the set of $$d$$-dimensional angles as $$(\theta_1,\Omega')$$, where
$$\Omega'$$ are the $$d-2$$ remaining angles parametrising $$S^{d-2}$$:

$$
\hat{\Delta}_d = \frac{1}{\sin^{d-2}\theta_1}\frac{\partial}{\partial\theta_1}\!\left(\sin^{d-2}\theta_1\frac{\partial}{\partial\theta_1}\right) + \frac{1}{\sin^2\theta_1}\hat{\Delta}_{d-1},
$$

with the base case $$\hat{\Lambda}_2^2 = \partial^2/\partial\varphi^2$$. For $$d=3$$ this
reproduces the familiar form

$$
\hat{\Lambda}_3^2 = \frac{1}{\sin\theta}\frac{\partial}{\partial\theta}\!\left(\sin\theta\frac{\partial}{\partial\theta}\right) + \frac{1}{\sin^2\theta}\frac{\partial^2}{\partial\varphi^2},
$$

consistent with $$\hat{\mathbf{L}}^2 = -\hbar^2\hat{\Lambda}_3^2$$.

---

### 4 Separation into Radial and Angular Parts

We now return to the time-independent Schrödinger equation for a central potential
$$V(\mathbf{r})=V(r)$$ and show how the radial and angular equations both emerge from a
single separation of variables.

#### 4.1 The Schrödinger equation in hyperspherical coordinates

A particle of mass $$m$$ in a central potential $$V(r)$$, with energy $$E > 0$$, satisfies

\begin{equation}\label{eq.schrodinger}
\left[-\frac{\hbar^2}{2m}\nabla_d^2 + V(r)\right]\psi(\mathbf{r}) = E\,\psi(\mathbf{r}).
\end{equation}

Defining $$k = \sqrt{2mE}/\hbar$$ and $$U(r) = 2mV(r)/\hbar^2$$, we rewrite it as
$$(\nabla_d^2 + k^2 - U)\psi = 0$$. Using the decomposition \eqref{eq.laplacian.d}:

$$
-\frac{\hbar^2}{2m}\left[\frac{1}{r^{d-1}}\frac{\partial}{\partial r}\!\left(r^{d-1}\frac{\partial\psi}{\partial r}\right) + \frac{1}{r^2}\hat{\Delta}_d\psi\right] + V(r)\psi = E\psi.
$$

Everything in this equation depends on both $$r$$ and the angular coordinates
$$\Omega = (\theta_1,\ldots,\theta_{d-2},\varphi)$$. The key observation is that $$V(r)$$
depends only on $$r$$, while $$\hat{\Delta}_d$$ acts only on $$\Omega$$.

#### 4.2 Spherical symmetry motivates the separation

A central potential $$V(r)$$ has a crucial geometric property: its level sets are
concentric spheres. Nothing in the problem distinguishes different directions — the
potential has the same value at every point of a given sphere. The consequence is that
the wave function separates as a product $$\psi(\mathbf{r}) = R(r)\,Y(\hat{\mathbf{r}})$$,
where $$R(r)$$ describes how the amplitude varies with distance (it senses the potential
$$V(r)$$) and $$Y(\hat{\mathbf{r}})$$ describes the angular pattern (sensing only the
geometry of the sphere — hence universal).

#### 4.3 The separation ansatz $$\psi = R(r)\,Y(\Omega)$$

Substituting $$\psi(r,\Omega) = R(r)\,Y(\Omega)$$ and dividing by $$RY$$ and multiplying
by $$-2mr^2/\hbar^2$$:

$$
\underbrace{\frac{r^2}{R}\frac{1}{r^{d-1}}\frac{\mathrm{d}}{\mathrm{d}r}\!\left(r^{d-1}\frac{\mathrm{d}R}{\mathrm{d}r}\right) - \frac{2m}{\hbar^2}[V(r)-E]\,r^2}_{\text{depends only on }r} = -\underbrace{\frac{1}{Y}\hat{\Delta}_d Y}_{\text{depends only on }\Omega}.
$$

The left-hand side is a function of $$r$$ alone; the right-hand side, of $$\Omega$$ alone.
Since they are equal for all $$r$$ and all $$\Omega$$, both must equal a common constant,
which we denote $$\lambda$$.

#### 4.4 The angular eigenvalue equation

Equating the right-hand side to $$\lambda$$:

\begin{equation}\label{eq.angular.eigenvalue}
\hat{\Delta}_d\,Y(\Omega) = -\lambda\,Y(\Omega).
\end{equation}

This is an eigenvalue equation for the Laplace–Beltrami operator on $$S^{d-1}$$: the
angular part of the wave function must be an eigenfunction of $$\hat{\Delta}_d$$ with
eigenvalue $$-\lambda$$. At this stage, $$\lambda$$ is an undetermined separation
constant; its admissible values will be fixed by the requirement that $$Y$$ be
single-valued and normalisable on $$S^{d-1}$$.

#### 4.5 The radial equation

Equating the left-hand side to $$\lambda$$, dividing by $$r^2$$ and restoring the original
form:

\begin{equation}\label{eq.radial}
-\frac{\hbar^2}{2m}\left[\frac{1}{r^{d-1}}\frac{\mathrm{d}}{\mathrm{d}r}\!\left(r^{d-1}\frac{\mathrm{d}R}{\mathrm{d}r}\right) - \frac{\lambda}{r^2}\,R\right] + V(r)\,R = E\,R.
\end{equation}

This is the radial Schrödinger equation in $$d$$ dimensions. The angular separation
constant $$\lambda$$ enters as a centrifugal-like term. Once the angular equation is
solved and $$\lambda = \ell(\ell+d-2)$$ is determined (which we shall do next),
\eqref{eq.radial} becomes a closed ODE for $$R(r)$$.

The angular equation \eqref{eq.angular.eigenvalue} is **universal**: it is the same for
every central potential, every energy, and even for bound states vs. scattering states
— it is purely a property of the geometry of the $$(d-1)$$-sphere. The radial equation,
by contrast, is where all the specific physics of a potential enters. We solve the
angular equation once (next) and then the radial equation separately for each $$V(r)$$
(Part II).

---

### 5 Hyperspherical Harmonics: Complete Derivation

Our task is to find all eigenvalues $$\lambda$$ and eigenfunctions $$Y(\Omega)$$ of the
angular equation \eqref{eq.angular.eigenvalue}. We proceed by successive separations of
variables, exploiting the recursive structure of $$\hat{\Delta}_d$$.

#### 5.1 The separation chain and the azimuthal equation

We carry out the first separation in full detail, identify the pattern, and follow the
chain down to the azimuthal angle $$\varphi$$.

**First separation: isolating $$\theta_1$$.** We seek eigenfunctions of $$\hat{\Delta}_d$$
on $$S^{d-1}$$. The equation $$\hat{\Delta}_d Y = -\lambda Y$$ becomes explicitly

$$
\frac{1}{\sin^{d-2}\theta_1}\frac{\partial}{\partial\theta_1}\!\left(\sin^{d-2}\theta_1\frac{\partial Y}{\partial\theta_1}\right) + \frac{1}{\sin^2\theta_1}\hat{\Delta}_{d-1}Y = -\lambda Y,
$$

where $$\hat{\Delta}_{d-1}$$ acts on the remaining $$d-2$$ angles
$$(\theta_2,\ldots,\theta_{d-2},\varphi)$$. We try the product ansatz

$$Y(\theta_1,\theta_2,\ldots,\varphi) = \Theta_1(\theta_1)\,Z(\theta_2,\ldots,\theta_{d-2},\varphi).$$

Substituting, dividing by $$\Theta_1 Z$$ and multiplying by $$\sin^2\theta_1$:

$$
\underbrace{\frac{\sin^2\theta_1}{\Theta_1}\frac{1}{\sin^{d-2}\theta_1}\frac{\mathrm{d}}{\mathrm{d}\theta_1}\!\left(\sin^{d-2}\theta_1\Theta_1'\right) + \lambda\sin^2\theta_1}_{\text{depends only on }\theta_1} = -\underbrace{\frac{1}{Z}\hat{\Delta}_{d-1}Z}_{\text{depends only on }(\theta_2,\ldots,\varphi)}.
$$

Both sides must equal a separation constant, $$\lambda^{(d-1)}$$. The right-hand side
gives

$$
\hat{\Delta}_{d-1}Z = -\lambda^{(d-1)}Z,
$$

which has the same structure as $$\hat{\Delta}_d Y = -\lambda Y$$, but in one fewer
dimension.

**The pattern: a chain of eigenvalue equations.** Applying the same procedure
successively, we generate a chain of factorisations:

$$
\begin{aligned}
Y^{(d)}(\theta_1,\theta_2,\ldots,\theta_{d-2},\varphi) &= \Theta_1(\theta_1)\cdot Y^{(d-1)}(\theta_2,\ldots,\varphi),\\
Y^{(d-1)}(\theta_2,\ldots,\varphi) &= \Theta_2(\theta_2)\cdot Y^{(d-2)}(\theta_3,\ldots,\varphi),\\
&\;\;\vdots\\
Y^{(3)}(\theta_{d-2},\varphi) &= \Theta_{d-2}(\theta_{d-2})\cdot\Phi(\varphi),
\end{aligned}
$$

and the complete eigenfunction is the product

$$Y^{(d)} = \Theta_1(\theta_1)\,\Theta_2(\theta_2)\cdots\Theta_{d-2}(\theta_{d-2})\,\Phi(\varphi).$$

**The last separation: the ODE for $$\Phi(\varphi)$$.** After $$d-3$$ separations of this
kind, we are left with the equation for $$\hat{\Lambda}_3^2$$ on $$S^2$$. A final
separation $$Y^{(3)} = \Theta_{d-2}(\theta_{d-2})\,\Phi(\varphi)$$ produces, for the
$$\varphi$$ part:

$$
\frac{\mathrm{d}^2\Phi}{\mathrm{d}\varphi^2} = -\lambda_\varphi\,\Phi.
$$

The equation for $$\Phi(\varphi)$$ is not assumed *a priori*: it emerges as the final
separation constant in the chain. Trying $$\Phi(\varphi) = \mathrm{e}^{\mathrm{i}\alpha\varphi}$$,
we find $$(i\alpha)^2 = -\alpha^2 = -\lambda_\varphi$$, hence $$\lambda_\varphi = \alpha^2$$
and $$\Phi(\varphi) = A\,\mathrm{e}^{\mathrm{i}\alpha\varphi} + B\,\mathrm{e}^{-\mathrm{i}\alpha\varphi}$$.

**Single-valuedness condition (periodicity).** The wave function must be single-valued:
$$\Phi(\varphi+2\pi) = \Phi(\varphi)$$. Applied to $$\mathrm{e}^{\mathrm{i}\alpha\varphi}$$:

$$
\mathrm{e}^{2\pi\mathrm{i}\alpha} = 1 \implies \alpha \in \mathbb{Z}.
$$

Taking $$\alpha = m$$ with $$m = 0,\pm 1,\pm 2,\ldots$$, we organise the solutions in the
normalised basis

$$
\Phi_m(\varphi) = \frac{\mathrm{e}^{\mathrm{i}m\varphi}}{\sqrt{2\pi}}, \qquad m\in\mathbb{Z}, \qquad \lambda_\varphi = m^2.
$$

This result holds in every dimension $$d\geq 2$$: the azimuthal angle always carries the
quantum number $$m\in\mathbb{Z}$$, and its separation constant is always $$m^2$$.

#### 5.2 The polar-angle equations: the general step

Each polar-angle equation has the same mathematical structure. Rather than repeating it
$$d-3$$ times, we formalise the general step by induction.

Suppose the eigenvalue problem on $$S^{d-2}$$ (the sphere parametrised by
$$\Omega' = (\theta_2,\ldots,\theta_{d-2},\varphi)$$) has already been solved — with the
azimuthal equation as the ultimate base case:

$$
\hat{\Delta}_{d-1}Y_{\ell'}^{(d-1)}(\Omega') = -\ell'(\ell'+d-3)\,Y_{\ell'}^{(d-1)}(\Omega'), \qquad \ell' = 0,1,2,\ldots
$$

We seek solutions of $$\hat{\Delta}_d Y = -\lambda Y$$ in the separated form
$$Y(\theta_1,\Omega') = \Theta(\theta_1)\,Y_{\ell'}^{(d-1)}(\Omega')$$. Substituting and
dividing by $$\Theta\,Y_{\ell'}^{(d-1)}$$:

$$
\frac{1}{\sin^{d-2}\theta_1}\frac{\mathrm{d}}{\mathrm{d}\theta_1}\!\left(\sin^{d-2}\theta_1\frac{\mathrm{d}\Theta}{\mathrm{d}\theta_1}\right) - \frac{\ell'(\ell'+d-3)}{\sin^2\theta_1}\Theta + \lambda\Theta = 0.
$$

This is the master ODE for each angular level. It remains to solve it.

#### 5.3 Change of variable: $$u = \cos\theta_1$$

Taking $$u = \cos\theta_1 \in [-1,1]$$, with $$\sin\theta_1 = \sqrt{1-u^2}$$ and
$$\mathrm{d}/\mathrm{d}\theta_1 = -\sin\theta_1\,\mathrm{d}/\mathrm{d}u$$, and writing
$$s \equiv \sin\theta_1 = \sqrt{1-u^2}$$, the master ODE transforms term by term. After
simplification, the equation becomes

$$
(1-u^2)\Theta'' - (d-1)\,u\Theta' + \left[\lambda - \frac{\ell'(\ell'+d-3)}{1-u^2}\right]\Theta = 0.
$$

#### 5.4 Extracting the singular behaviour

This equation has regular singular points at $$u = \pm 1$$ (the poles of the sphere). The
term $$\ell'(\ell'+d-3)/(1-u^2)$$ diverges there, so we extract the expected singular
behaviour by writing

$$
\Theta(u) = (1-u^2)^{\sigma/2}\,P(u),
$$

with $$\sigma \equiv \ell'$$. This is the $$d$$-dimensional generalisation of the standard
3D trick, in which the solution of the associated Legendre equation is written as
$$(1-u^2)^{|m|/2}$$ times a polynomial. After substitution, the singular terms in
$$1/(1-u^2)$$ cancel exactly (the key point that makes the ansatz work), and the
resulting ODE for $$P(u)$$ is

\begin{equation}\label{eq.gegenbauer.ode}
(1-u^2)\,P'' - (2\sigma+d-1)\,u\,P' + \left[\lambda - \sigma(\sigma+d-2)\right]P = 0,
\end{equation}

with $$\sigma = \ell'$$.

#### 5.5 Identification as the Gegenbauer equation and quantisation

The standard **Gegenbauer (ultraspherical) equation** with parameter $$\alpha > 0$$ and
degree $$n$$ is

\begin{equation}\label{eq.gegenbauer.standard}
(1-u^2)\,P'' - (2\alpha+1)\,u\,P' + n(n+2\alpha)\,P = 0.
\end{equation}

Comparing \eqref{eq.gegenbauer.ode} with \eqref{eq.gegenbauer.standard}:

$$
2\alpha+1 = 2\sigma+d-1 \implies \alpha = \sigma + \frac{d-2}{2} = \ell' + \frac{d-2}{2},
$$

$$
n(n+2\alpha) = \lambda - \sigma(\sigma+d-2).
$$

Equation \eqref{eq.gegenbauer.standard} has polynomial solutions — the **Gegenbauer
polynomials** $$C_n^{(\alpha)}(u)$$ — if and only if $$n$$ is a non-negative integer.
Otherwise, the series solution diverges at $$u = \pm 1$$, producing functions that are
not normalisable on $$S^{d-1}$$.

We therefore require $$n \in \{0,1,2,\ldots\}$$. Define $$\ell \equiv n + \sigma = n + \ell'$$,
that is,

$$
n = \ell - \ell', \qquad \ell \geq \ell' \geq 0.
$$

Solving for $$\lambda$$:

$$
\lambda = n(n+2\alpha) + \sigma(\sigma+d-2) = \ell^2 + \ell(d-2) = \ell(\ell+d-2).
$$

We conclude:

\begin{equation}\label{eq.angular.eigenvalue.result}
\hat{\Delta}_d\,Y_\ell^{(d)}(\Omega) = -\ell(\ell+d-2)\,Y_\ell^{(d)}(\Omega), \qquad \ell = 0,1,2,\ldots
\end{equation}

The eigenvalue $$\lambda = \ell(\ell+d-2)$$ depends only on $$\ell$$ and $$d$$, and is
independent of $$\ell'$$ and the other lower quantum numbers. This is the counterpart of
the familiar fact in $$d=3$$ that the eigenvalue $$\ell(\ell+1)$$ of $$\hat{\mathbf{L}}^2$$
does not depend on $$m$$. For $$d=3$$: $$\lambda = \ell(\ell+1)$$. For $$d=2$$:
$$\lambda = \ell^2 = m^2$$, in agreement with the base case.

#### 5.6 The complete angular eigenfunctions

Putting all the pieces together, the normalised solution of the $$\theta_1$$ equation is

$$
\Theta_{\ell,\ell'}(\theta_1) = \mathcal{N}_{\ell,\ell'}^{(d)}\,\sin^{\ell'}\!\theta_1\;C_{\ell-\ell'}^{\ell'+(d-2)/2}(\cos\theta_1),
$$

where $$C_n^{(\alpha)}$$ is the Gegenbauer polynomial and $$\mathcal{N}_{\ell,\ell'}^{(d)}$$
is the normalisation constant fixed by $$\int_0^\pi |\Theta_{\ell,\ell'}|^2\sin^{d-2}\theta_1\,\mathrm{d}\theta_1 = 1$$.

The **full hyperspherical harmonic** is then constructed recursively as

$$
Y_{\ell_1\ell_2\cdots\ell_{d-2}m}^{(d)}(\theta_1,\ldots,\theta_{d-2},\varphi) = \prod_{j=1}^{d-2}\Theta_{\ell_j,\ell_{j+1}}^{(j)}(\theta_j)\cdot\frac{\mathrm{e}^{\mathrm{i}m\varphi}}{\sqrt{2\pi}},
$$

with $$\ell_{d-1} \equiv |m|$$ and each factor $$\Theta^{(j)}$$ in the appropriate
form with the dimension and quantum numbers appropriate to the $$j$$-th level of the
recursion.

For $$d=3$$, the complete quantum numbers are $$(\ell_1,m) = (\ell,m)$$, and the single
$$\Theta$$ factor is $$\Theta_{\ell,|m|}(\theta) \propto \sin^{|m|}\theta\;C_{\ell-|m|}^{|m|+1/2}(\cos\theta)$$.
The Gegenbauer polynomial $$C_n^{|m|+1/2}(\cos\theta)$$ is proportional to the
associated Legendre function $$P_\ell^{|m|}(\cos\theta)$$, recovering the standard
spherical harmonic.

#### 5.7 Quantum numbers and degeneracy

A complete set of quantum numbers labelling a hyperspherical harmonic on $$S^{d-1}$$ is
$$(\ell_1,\ell_2,\ldots,\ell_{d-2},m)$$, subject to the nesting condition

$$
\ell \equiv \ell_1 \geq \ell_2 \geq \cdots \geq \ell_{d-2} \geq |m| \geq 0, \qquad m\in\mathbb{Z}.
$$

The degeneracy $$N(\ell,d)$$ — the number of linearly independent harmonics for a given
$$\ell$$ on $$S^{d-1}$$ — is obtained by counting these sequences. The result, derived by
induction in $$d$$, is

\begin{equation}\label{eq.degeneracy}
N(\ell,d) = \frac{(2\ell+d-2)(\ell+d-3)!}{\ell!\,(d-2)!}, \qquad \ell \geq 0.
\end{equation}

For $$d=3$$: $$N(\ell,3) = 2\ell+1$$ (the familiar set of spherical harmonics $$Y_\ell^m$$
with $$m=-\ell,\ldots,+\ell$$). For $$d=4$$: $$N(\ell,4) = (\ell+1)^2$$, the well-known
degeneracy on $$S^3$$.

---

### 6 The Radial Equation: Further Development

#### 6.1 The radial equation with the angular eigenvalue inserted

Having solved the angular problem, we substitute $$\lambda = \ell(\ell+d-2)$$ into
\eqref{eq.radial}. Expanding the radial derivative:

\begin{equation}\label{eq.radial.full}
-\frac{\hbar^2}{2m}\left[\frac{\mathrm{d}^2 R}{\mathrm{d}r^2} + \frac{d-1}{r}\frac{\mathrm{d}R}{\mathrm{d}r} - \frac{\ell(\ell+d-2)}{r^2}\,R\right] + V(r)\,R = E\,R.
\end{equation}

#### 6.2 Reduction to an effective one-dimensional problem

It is convenient to eliminate the first-derivative term by substituting

\begin{equation}\label{eq.R.to.u}
R(r) = \frac{u(r)}{r^{(d-1)/2}}.
\end{equation}

One verifies by direct differentiation that, if $$R$$ satisfies \eqref{eq.radial.full},
then $$u(r)$$ satisfies

\begin{equation}\label{eq.radial.1d}
-\frac{\hbar^2}{2m}\frac{\mathrm{d}^2 u}{\mathrm{d}r^2} + \left[V(r) + \frac{\hbar^2}{2m}\frac{\mathcal{L}(\mathcal{L}+1)}{r^2}\right]u = E\,u,
\end{equation}

with the **effective angular-momentum parameter**

\begin{equation}\label{eq.calL}
\mathcal{L} \equiv \ell + \frac{d-3}{2}.
\end{equation}

For the derivation, substituting $$R = u/r^{(d-1)/2}$$ and collecting terms, the
centrifugal contribution from $$\ell(\ell+d-2)$$ and the geometric correction
from the first-derivative elimination combine to give

$$
\frac{\ell(\ell+d-2) + \frac{(d-1)(d-3)}{4}}{r^2} = \frac{\left(\ell+\frac{d-3}{2}\right)\!\left(\ell+\frac{d-1}{2}\right)}{r^2} = \frac{\mathcal{L}(\mathcal{L}+1)}{r^2},
$$

with $$\mathcal{L} = \ell + (d-3)/2$$, confirming \eqref{eq.radial.1d} and \eqref{eq.calL}.

Equation \eqref{eq.radial.1d} has **exactly** the form of the one-dimensional radial
Schrödinger equation in three dimensions, but with the angular-momentum quantum number
$$\ell$$ replaced by $$\mathcal{L} = \ell + (d-3)/2$$. This is the key structural
observation: the central-potential problem in $$d$$ dimensions maps onto a family of
effective 1D problems labelled by $$\mathcal{L}$$.

#### 6.3 Normalisation condition and effective potential

Since $$\mathrm{d}^d r = r^{d-1}\,\mathrm{d}r\,\mathrm{d}\Omega_d$$ and the hyperspherical
harmonics are orthonormal on $$S^{d-1}$$, the normalisation of the full wave function
reduces to $$\int_0^\infty |u(r)|^2\,\mathrm{d}r = 1$$, and $$u(r)$$ plays the role of
a standard wave function in $$L^2(0,\infty)$$. The boundary conditions are $$u(0) = 0$$
(regularity at the origin, since $$R = u/r^{(d-1)/2}$$ must be finite) and
$$u(r) \to 0$$ as $$r\to\infty$$ (for bound states).

For any central potential, the reduced equation \eqref{eq.radial.1d} involves the
effective potential

$$
V_{\mathrm{eff}}(r) = V(r) + \frac{\hbar^2}{2m}\frac{\mathcal{L}(\mathcal{L}+1)}{r^2}.
$$

The centrifugal barrier $$\propto 1/r^2$$ grows both with $$\ell$$ and with $$d$$. In the
scattering problem, it dominates near the origin (except in $$d=2$$ with $$\ell=0$$).

#### 6.4 Reduction to the Bessel equation

Setting $$V=0$$ in \eqref{eq.radial.1d} and using $$\rho = kr$$, with the notation
$$\lambda = \ell + \nu = \mathcal{L} + \tfrac{1}{2}$$ (caution: $$\lambda$$ here is the
order of the Bessel function, distinct from the angular separation constant used in §4):

$$
\frac{\mathrm{d}^2 u_\ell}{\mathrm{d}\rho^2} + \left[1 - \frac{\lambda^2 - \frac{1}{4}}{\rho^2}\right]u_\ell = 0.
$$

The substitution $$u_\ell = \sqrt{\rho}\,w$$ converts this equation into the **Bessel
equation of order $$\lambda$$**:

\begin{equation}\label{eq.bessel}
\rho^2 w'' + \rho w' + (\rho^2 - \lambda^2)w = 0.
\end{equation}

Equation \eqref{eq.bessel} is a second-order ODE, and therefore admits two linearly
independent solutions:

- $$J_\lambda(\rho)$$, the **Bessel function of the first kind**, defined by the series

$$
J_\lambda(\rho) = \sum_{n=0}^\infty \frac{(-1)^n}{n!\,\Gamma(n+\lambda+1)}\!\left(\frac{\rho}{2}\right)^{\!2n+\lambda}.
$$

It is regular at the origin, with behaviour $$J_\lambda(\rho) \sim \rho^\lambda/[2^\lambda\Gamma(\lambda+1)]$$ as $$\rho\to 0$$, and oscillates as $$\sim\sqrt{2/(\pi\rho)}$$ at large $$\rho$$.

- $$N_\lambda(\rho)$$, the **Bessel function of the second kind**, or **Neumann function**, defined by the linear combination

$$
N_\lambda(\rho) = \frac{\cos(\lambda\pi)\,J_\lambda(\rho) - J_{-\lambda}(\rho)}{\sin(\lambda\pi)}
$$

(with the definition extended by limit when $$\lambda$$ is an integer). It is *singular*
at the origin, diverging as $$N_\lambda(\rho) \sim -2^\lambda\Gamma(\lambda)/(\pi\rho^\lambda)$$
as $$\rho\to 0$$. It also oscillates at large $$\rho$$, but with phase shifted by $$\pi/2$$
relative to $$J_\lambda$$.

Returning to the variable $$u_\ell = \sqrt{\rho}\,w$$, the two linearly independent solutions
of the free radial equation are:

$$
u_\ell^{(1)}(\rho) = \sqrt{\rho}\,J_\lambda(\rho) \quad (\text{regular at }\rho=0), \qquad u_\ell^{(2)}(\rho) = \sqrt{\rho}\,N_\lambda(\rho) \quad (\text{singular at }\rho=0).
$$

#### 6.5 Asymptotic behaviour

As $$\rho\to\infty$$, using $$J_\lambda(\rho)\sim\sqrt{2/(\pi\rho)}\cos(\rho-\lambda\pi/2-\pi/4)$$:

$$
\sqrt{\rho}\,J_\lambda(\rho) \xrightarrow{\rho\to\infty} \sqrt{\frac{2}{\pi}}\sin\!\left(\rho - \frac{\ell\pi}{2} - \frac{(d-3)\pi}{4}\right),
$$

by the identity $$\cos(\rho - \lambda\pi/2 - \pi/4) = \sin(\rho - \ell\pi/2 - (d-3)\pi/4)$$
which follows from $$\lambda\pi/2 + \pi/4 = \ell\pi/2 + (d-1)\pi/4$$. Similarly,
$$\sqrt{\rho}\,N_\lambda \to -\sqrt{2/\pi}\cos(\rho - \ell\pi/2 - (d-3)\pi/4)$$.

As $$\rho\to 0$$:

$$
J_\lambda(\rho) \sim \frac{\rho^\lambda}{2^\lambda\Gamma(\lambda+1)}, \qquad N_\lambda(\rho) \sim -\frac{2^\lambda\Gamma(\lambda)}{\pi\rho^\lambda}.
$$

For a free particle everywhere, $$N_\lambda$$ is excluded by regularity at the origin.
But in scattering, $$N_\lambda$$ appears in the exterior region ($$r > R_0$$, where
$$V = 0$$) because the origin is *inside* the potential region. The amount of $$N_\lambda$$
mixed in encodes the phase shift.

For compactness, we define

$$
\hat{j}_\ell^{(d)}(\rho) \equiv \frac{J_{\ell+\nu}(\rho)}{(\rho/2)^\nu},
$$

the natural generalisation of the spherical Bessel function in $$d$$ dimensions. In
$$d=3$$ it reduces to $$\sqrt{2/\pi}\,j_\ell(\rho)$$.

---

### 7 The Rayleigh Expansion of the Plane Wave

We now derive a central result: the decomposition of a plane wave into partial waves.

#### 7.1 Statement and strategy

The result to be established is

\begin{equation}\label{eq.rayleigh}
\mathrm{e}^{\mathrm{i}kr\cos\theta} = \Gamma(\nu)\sum_{\ell=0}^\infty (\ell+\nu)\,\mathrm{i}^\ell\,\hat{j}_\ell^{(d)}(kr)\,C_\ell^\nu(\cos\theta).
\end{equation}

By axial symmetry, $$\mathrm{e}^{\mathrm{i}\rho\cos\theta}$$ (with $$\rho = kr$$) depends
only on $$r$$ and $$\theta$$, and so expands as
$$\mathrm{e}^{\mathrm{i}\rho\cos\theta} = \sum_\ell a_\ell(\rho)\,C_\ell^\nu(\cos\theta)$$.
Gegenbauer orthogonality gives the coefficients:

$$
a_\ell(\rho) = \frac{1}{h_\ell^{(\nu)}}\,I_\ell(\rho), \qquad I_\ell(\rho) \equiv \int_{-1}^1 \mathrm{e}^{\mathrm{i}\rho x}\,C_\ell^\nu(x)\,(1-x^2)^{\nu-1/2}\mathrm{d}x,
$$

where $$h_\ell^{(\nu)} = \pi\,2^{1-2\nu}\Gamma(\ell+2\nu)/[\ell!\,(\ell+\nu)\Gamma(\nu)^2]$$.
The whole derivation reduces to evaluating $$I_\ell(\rho)$$.

#### 7.2 Evaluation of $$I_\ell(\rho)$$

**Step 1: Apply Rodrigues' formula.** The Rodrigues formula for the Gegenbauer
polynomials allows us to write

$$
I_\ell = \frac{(-1)^\ell}{2^\ell\,\ell!}\frac{\Gamma(\nu+\frac{1}{2})\,\Gamma(\ell+2\nu)}{\Gamma(2\nu)\,\Gamma(\ell+\nu+\frac{1}{2})} \int_{-1}^1 \mathrm{e}^{\mathrm{i}\rho x}\frac{\mathrm{d}^\ell}{\mathrm{d}x^\ell}\!\left[(1-x^2)^{\ell+\nu-1/2}\right]\mathrm{d}x,
$$

after cancellation of the weight $$(1-x^2)^{\nu-1/2}$$ against $$(1-x^2)^{-(\nu-1/2)}$$
from the formula.

**Step 2: Integrate by parts $$\ell$$ times.** The boundary terms vanish, since
$$(1-x^2)^{\ell+\nu-1/2}$$ and its derivatives up to order $$\ell-1$$ vanish at
$$x=\pm 1$$. Each integration by parts produces a factor $$-\mathrm{i}\rho$$:

$$
I_\ell = \frac{(\mathrm{i}\rho)^\ell}{2^\ell\,\ell!}\frac{\Gamma(\nu+\frac{1}{2})\,\Gamma(\ell+2\nu)}{\Gamma(2\nu)\,\Gamma(\ell+\nu+\frac{1}{2})}\,\mathcal{J}_\mu(\rho),
$$

with $$\mathcal{J}_\mu(\rho) = \int_{-1}^1 \mathrm{e}^{\mathrm{i}\rho x}(1-x^2)^\mu\,\mathrm{d}x$$ and
$$\mu = \ell + \nu - \tfrac{1}{2}$$.

**Step 3: Compute $$\mathcal{J}_\mu(\rho)$$ via series.** Since $$(1-x^2)^\mu$$ is even,
only the cosine part contributes. Expanding $$\cos(\rho x)$$ in series and using the
Beta function for the integrals $$\int_0^1 x^{2n}(1-x^2)^\mu\,\mathrm{d}x$$, one
identifies the Bessel-function series:

$$
\mathcal{J}_\mu(\rho) = \frac{\sqrt{\pi}\,\Gamma(\mu+1)}{(\rho/2)^{\mu+1/2}}\,J_{\mu+1/2}(\rho).
$$

**Step 4: Substitute and simplify.** With $$\mu + \tfrac{1}{2} = \lambda = \ell+\nu$$
and $$\Gamma(\mu+1) = \Gamma(\ell+\nu+\tfrac{1}{2})$$, the cancellations give

$$
I_\ell(\rho) = \mathrm{i}^\ell\,\frac{\sqrt{\pi}\,\Gamma(\nu+\frac{1}{2})\,\Gamma(\ell+2\nu)}{2^\nu\,\ell!\,\Gamma(2\nu)}\,\hat{j}_\ell^{(d)}(\rho).
$$

**Step 5: Compute $$a_\ell = I_\ell/h_\ell^{(\nu)}$$.** Applying the Legendre duplication
formula $$\Gamma(2\nu) = 2^{2\nu-1}\Gamma(\nu)\Gamma(\nu+\tfrac{1}{2})/\sqrt{\pi}$$ and
simplifying the $$\Gamma$$ factors and powers of 2:

$$
a_\ell(\rho) = \Gamma(\nu)\,(\ell+\nu)\,\mathrm{i}^\ell\,\hat{j}_\ell^{(d)}(\rho),
$$

which substituted into the expansion gives \eqref{eq.rayleigh}.

#### 7.3 Physical interpretation

Each partial wave $$\ell$$ in the plane wave carries: an angular pattern
$$C_\ell^\nu(\cos\theta)$$; a radial function $$\hat{j}_\ell^{(d)}(kr)$$ — the regular
free solution (regular because the plane wave is well-behaved at $$r=0$$); a weight
$$(\ell+\nu)$$ — the amount of angular momentum $$\ell$$ present; and a kinematic phase
$$\mathrm{i}^\ell$$. The absence of $$N_\lambda$$ is crucial: when a potential introduces
a mixture of $$N_\lambda$$ in the exterior region, that mixture is due entirely to
scattering.

---

### 8 The Scattering Framework

This section is universal: it applies to any short-range central potential. The specific
potential enters only through the phase shifts $$\delta_\ell$$.

#### 8.1 The scattering boundary condition

At large distances from the target, the scattering wave function must take the form

\begin{equation}\label{eq.asymptotic.bc}
\psi(\mathbf{r}) \xrightarrow{r\to\infty} \mathrm{e}^{ikz} + f(\theta)\,\frac{\mathrm{e}^{ikr}}{r^{(d-1)/2}},
\end{equation}

where $$z = r\cos\theta$$ and $$f(\theta)$$ is the **scattering amplitude**. This
condition is the starting point of the entire theory and deserves justification at three
levels: the physical meaning of each term, the origin of the exponent $$1/r^{(d-1)/2}$$
via probability conservation, and the formal justification via the Green's function.

**Physical meaning of each term.** We prepare a particle very far from the target,
with a well-defined momentum $$\mathbf{p} = \hbar k\hat{\mathbf{e}}_d$$ along the beam
axis. Before the interaction, it is described by a plane wave $$\mathrm{e}^{ikz}$$ — a
momentum eigenstate, propagating in the $$+z$$ direction. After interacting with
$$V(r)$$, an additional component arises: the *outgoing wave*, which propagates radially
outward from the scattering centre. Since the potential is central and the beam has
axial symmetry around the beam axis, the outgoing wave carries an angular distribution
$$f(\theta)$$, the scattering amplitude, encoding how much flux exits in each direction.

**Origin of the exponent $$1/r^{(d-1)/2}$$: probability conservation.** The power
$$1/r^{(d-1)/2}$$ is not conventional: it is the only one compatible with flux
conservation in $$d$$ dimensions. Consider a generic spherical wave
$$\psi_{\mathrm{sc}}(\mathbf{r}) \sim A(\theta)\,\mathrm{e}^{ikr}/r^\alpha$$ with
exponent $$\alpha$$ to be determined. The probability current density is
$$\mathbf{j} = (\hbar/m)\,\mathrm{Im}[\psi^*\nabla\psi]$$. Computing the radial component
at large $$r$$:

$$
j_r = \frac{\hbar k}{m}\frac{|A(\theta)|^2}{r^{2\alpha}}.
$$

The rate of particles crossing a sphere of radius $$r$$ per unit time is

$$
\mathrm{d}\dot{N} = j_r\,\mathrm{d}A = v\,|A(\theta)|^2\frac{r^{d-1}}{r^{2\alpha}}\,\mathrm{d}\Omega_{d-1}.
$$

For this rate to be *finite and independent of $$r$$* — required by probability
conservation — the exponent in $$r$$ must cancel:

$$
r^{d-1-2\alpha} = \text{const} \implies d-1-2\alpha = 0 \implies \boxed{\alpha = \frac{d-1}{2}}.
$$

Checking familiar cases: in $$d=3$$, $$\alpha = 1$$, recovering the usual $$\mathrm{e}^{ikr}/r$$.
In $$d=2$$, $$\alpha = 1/2$$, giving $$\mathrm{e}^{ikr}/\sqrt{r}$$ — the cylindrical wave of
planar diffraction problems. In $$d=4$$, $$\alpha = 3/2$$.

**Formal justification: the Green's function.** The Schrödinger equation can be
rewritten as an inhomogeneous equation for the free part,
$$(\nabla_d^2 + k^2)\psi(\mathbf{r}) = U(r)\psi(\mathbf{r})$$, with $$U = 2mV/\hbar^2$$
treated as a "source". The formal solution is

$$
\psi(\mathbf{r}) = \psi_0(\mathbf{r}) + \int G_+(\mathbf{r},\mathbf{r}')\,U(r')\,\psi(\mathbf{r}')\,\mathrm{d}^d r',
$$

where $$\psi_0 = \mathrm{e}^{ikz}$$ is the free incident wave and $$G_+$$ is the
**retarded Green's function** of the Helmholtz operator $$(\nabla_d^2 + k^2)$$, defined
by $$(\nabla_d^2+k^2)G_+(\mathbf{r},\mathbf{r}') = \delta^{(d)}(\mathbf{r}-\mathbf{r}')$$,
with the condition that $$G_+$$ contains only *outgoing* waves (hence the $$+$$
subscript). In $$d$$ dimensions, $$G_+$$ can be written in closed form using Hankel
functions, and its asymptotic behaviour for $$r \gg r'$$ is

$$
G_+(\mathbf{r},\mathbf{r}') \xrightarrow{r\to\infty} -\frac{C_d}{r^{(d-1)/2}}\,\mathrm{e}^{ikr}\,\mathrm{e}^{-\mathrm{i}\mathbf{k}'\cdot\mathbf{r}'}, \qquad \mathbf{k}' \equiv k\hat{\mathbf{r}},
$$

where $$C_d$$ is a constant depending only on $$d$$. For $$d=3$$:
$$G_+(\mathbf{r},\mathbf{r}') = -\mathrm{e}^{\mathrm{i}k|\mathbf{r}-\mathbf{r}'|}/(4\pi|\mathbf{r}-\mathbf{r}'|)$$,
which for $$|\mathbf{r}| \gg |\mathbf{r}'|$$ is approximately
$$-\mathrm{e}^{ikr}\mathrm{e}^{-\mathrm{i}\mathbf{k}'\cdot\mathbf{r}'}/(4\pi r)$$,
recovering $$\alpha = 1 = (d-1)/2$$. The key property is that the exponent in $$r$$ is
$$1/r^{(d-1)/2}$$ already inside the Green's function — it is not a choice imposed
*a posteriori*, it is a property of the Helmholtz operator in $$d$$ dimensions.
Substituting the asymptotics of $$G_+$$:

$$
\psi(\mathbf{r}) \xrightarrow{r\to\infty} \mathrm{e}^{ikz} + \underbrace{\left[-C_d\int \mathrm{e}^{-\mathrm{i}\mathbf{k}'\cdot\mathbf{r}'}\,U(r')\,\psi(\mathbf{r}')\,\mathrm{d}^d r'\right]}_{\equiv f(\theta)}\frac{\mathrm{e}^{ikr}}{r^{(d-1)/2}}.
$$

**Conclusion.** The boundary condition \eqref{eq.asymptotic.bc} is not an arbitrary
postulate: it is the unique asymptotic form compatible with (i) the presence of an
incident plane wave, (ii) probability conservation in $$d$$ dimensions, and (iii) the
choice of outgoing solutions (causality) of the Helmholtz equation. The three arguments
coincide because they express the same physical fact in different ways.

#### 8.2 Phase shifts: definition

The reduced radial solution in the exterior ($$V \approx 0$$) is a combination of the
two free solutions. The **phase shift** $$\delta_\ell(k)$$ is defined by the asymptotic
form

\begin{equation}\label{eq.phase.shift.def}
u_\ell(r) \xrightarrow{r\to\infty} C_\ell\sin\!\left(kr - \frac{\ell\pi}{2} - \frac{(d-3)\pi}{4} + \delta_\ell\right).
\end{equation}

Here $$C_\ell$$ is a normalisation constant of the reduced radial function (not to be
confused with the Gegenbauer polynomial $$C_\ell^\nu$$, which carries the superscript
$$\nu$$): since the radial equation is linear of second order, the asymptotic form is
characterised by two parameters — the amplitude $$C_\ell$$ and the phase $$\delta_\ell$$.
All the physical information of the scattering in the partial wave $$\ell$$ is contained
in $$\delta_\ell$$; the constant $$C_\ell$$ will be fixed *a posteriori* by matching with
the plane-wave expansion (§8.4). For a free particle, $$\delta_\ell = 0$$ for all $$\ell$$.

#### 8.3 Computing $$\delta_\ell$$ from a given $$V(r)$$

The matching procedure involves three steps. First, one solves the reduced equation
\eqref{eq.radial.1d} in the interior ($$r < R_0$$) with $$u_\ell(0) = 0$$ and the
specific $$V(r)$$. Second, one computes the logarithmic derivative at $$r = R_0$$:

$$
\gamma_\ell \equiv \frac{u_\ell'(R_0)}{u_\ell(R_0)}.
$$

Third, one matches with the exterior solution
$$u_\ell^{\mathrm{ext}}(r) = A[\sqrt{kr}\,J_\lambda(kr)\cos\delta_\ell - \sqrt{kr}\,N_\lambda(kr)\sin\delta_\ell]$$
at $$r = R_0$$. Continuity of $$u_\ell'/u_\ell$$ gives

\begin{equation}\label{eq.tan.delta}
\tan\delta_\ell = \frac{[\sqrt{\rho}\,J_\lambda(\rho)]'\big|_{\rho_0} - \gamma_\ell\sqrt{\rho_0}\,J_\lambda(\rho_0)/k}{[\sqrt{\rho}\,N_\lambda(\rho)]'\big|_{\rho_0} - \gamma_\ell\sqrt{\rho_0}\,N_\lambda(\rho_0)/k}, \qquad \rho_0 = kR_0.
\end{equation}

#### 8.4 Phase shifts $$\to$$ scattering amplitude: matching

This is the crucial derivation that produces $$f(\theta)$$ from the $$\delta_\ell$$. We
have three ingredients:

(i) The full wave function in partial waves:

$$
\psi(\mathbf{r}) = \sum_\ell a_\ell\,\frac{u_\ell(r)}{r^{(d-1)/2}}\,C_\ell^\nu(\cos\theta),
$$

with $$u_\ell \sim C_\ell\sin(kr - \phi_\ell + \delta_\ell)$$ at large $$r$$, where
$$\phi_\ell \equiv \ell\pi/2 + (d-3)\pi/4$$.

(ii) The plane wave in partial waves (Rayleigh expansion), with asymptotic form

$$
\mathrm{e}^{ikz} \sim \sum_\ell \Gamma(\nu)(\ell+\nu)\mathrm{i}^\ell\cdot\frac{\mathcal{N}}{(kr)^{\nu+1/2}}\sin(kr-\phi_\ell)\,C_\ell^\nu(\cos\theta),
$$

where $$\mathcal{N} = 2^\nu\sqrt{2/\pi}$$ is the asymptotic constant.

(iii) The scattered wave $$f(\theta)\,\mathrm{e}^{ikr}/r^{(d-1)/2}$$ is purely outgoing.

**Step 1: Decompose into incoming and outgoing waves.** Writing each
$$\sin(X) = (\mathrm{e}^{\mathrm{i}X} - \mathrm{e}^{-\mathrm{i}X})/(2\mathrm{i})$$, the incoming
coefficients of the full wave and the plane wave must match exactly (since the scattered
wave is purely outgoing). For each $$\ell$$, equating and cancelling common factors:

$$
a_\ell C_\ell\,\mathrm{e}^{-\mathrm{i}\delta_\ell} = \frac{\Gamma(\nu)(\ell+\nu)\,\mathrm{i}^\ell\,\mathcal{N}}{k^{\nu+1/2}},
$$

which on isolating $$a_\ell C_\ell$$ gives

\begin{equation}\label{eq.aC}
a_\ell C_\ell = \frac{\Gamma(\nu)(\ell+\nu)\,\mathrm{i}^\ell\,\mathcal{N}}{k^{\nu+1/2}}\,\mathrm{e}^{\mathrm{i}\delta_\ell}.
\end{equation}

**Step 2: Read off $$f(\theta)$$ from the outgoing excess.** The outgoing coefficient
in the full wave minus that in the plane wave gives the scattered wave. Using
\eqref{eq.aC}, and absorbing the kinematic factors into a single prefactor

$$
A_d \equiv \frac{2^\nu\sqrt{2/\pi}\,\Gamma(\nu)\,\mathrm{e}^{-\mathrm{i}(d-3)\pi/4}}{k^{1/2}},
$$

we arrive at the final result:

\begin{equation}\label{eq.f.theta}
\boxed{f(\theta) = \frac{A_d}{k^\nu}\sum_{\ell=0}^\infty (\ell+\nu)\,\mathrm{e}^{\mathrm{i}\delta_\ell}\sin\delta_\ell\,C_\ell^\nu(\cos\theta).}
\end{equation}

#### 8.5 Physical picture

The plane wave is a superposition of incoming and outgoing spherical waves in each
partial wave. The potential shifts the phase of the outgoing part by $$2\delta_\ell$$;
the incoming part is left untouched. The scattered wave is the outgoing excess. For
$$\delta_\ell = 0$$, the factor $$\mathrm{e}^{2\mathrm{i}\delta_\ell} - 1$$ vanishes, and
there is no scattering. For $$\delta_\ell = \pi/2$$, the factor equals $$2\mathrm{i}$$,
attaining the unitarity limit.

#### 8.6 Cross sections

The **differential cross section** is the ratio of the rate of particles scattered per
unit solid angle to the incident flux:

$$
\frac{\mathrm{d}\sigma}{\mathrm{d}\Omega} = |f(\theta)|^2.
$$

For the plane wave $$\psi_{\mathrm{inc}} = \mathrm{e}^{ikz}$$, the probability current
is $$\mathbf{j}_{\mathrm{inc}} = (\hbar k/m)\hat{\mathbf{e}}_d = v\hat{\mathbf{e}}_d$$,
and $$j_{\mathrm{inc}} = v$$. For
$$\psi_{\mathrm{sc}} \sim f(\theta)\,\mathrm{e}^{ikr}/r^{(d-1)/2}$$, the radial
component of the current at the detector is $$j_r^{\mathrm{sc}} = v|f(\theta)|^2/r^{d-1}$$,
and the rate of particles through $$\mathrm{d}A = r^{d-1}\,\mathrm{d}\Omega$$ is
$$\dot{N}_{\mathrm{sc}}\,\mathrm{d}\Omega = v|f(\theta)|^2\,\mathrm{d}\Omega$$. The
$$r^{d-1}$$ from the area cancels exactly the $$r^{-(d-1)}$$ from $$|\psi_{\mathrm{sc}}|^2$$
— the reason the envelope was chosen $$1/r^{(d-1)/2}$$.

The **total cross section**, using Gegenbauer orthogonality, is

\begin{equation}\label{eq.total.cross.section}
\sigma_{\mathrm{tot}} = \frac{\omega_{d-1}|A_d|^2}{k^{2\nu}}\sum_{\ell=0}^\infty (\ell+\nu)^2\sin^2\!\delta_\ell\;h_\ell^{(\nu)},
\end{equation}

and the **optical theorem** gives $$\sigma_{\mathrm{tot}} \propto \mathrm{Im}[f(0)]/k^\nu$$.

#### 8.7 Low-energy limit

For a finite-range potential,

$$
\delta_\ell(k) \sim k^{2\lambda} = k^{2\ell+d-2} \qquad \text{as } k\to 0.
$$

At low energy, only $$\ell = 0$$ survives (for $$d \geq 3$$). We define the **scattering
length**

$$
a_d^{d-2} \equiv -\lim_{k\to 0}\frac{\tan\delta_0}{k^{d-2}},
$$

with the effective-range expansion (for $$d\geq 3$$)
$$k^{d-2}\cot\delta_0 = -1/a_d^{d-2} + \tfrac{1}{2}r_d\,k^2 + \mathcal{O}(k^4)$$.
For $$d=2$$, $$\lambda_0 = 0$$ and the threshold behaviour is logarithmic
($$\delta_0 \sim -1/\ln ka$$), requiring separate treatment.

---

## Part II — Specific Potentials

We now apply the procedure to several potentials.

---

### 9 Hard Sphere: $$V(r) = \infty$$ for $$r < a$$

The hard wall imposes $$u_\ell(a) = 0$$. The exterior solution satisfies this condition
when

\begin{equation}\label{eq.hard.sphere}
\tan\delta_\ell = \frac{J_\lambda(ka)}{N_\lambda(ka)}.
\end{equation}

At low energy, using the small-argument asymptotics \eqref{eq.bessel}:
$$\tan\delta_\ell \sim (ka)^{2\lambda} = (ka)^{2\ell+d-2}$$, confirming the threshold
behaviour. The s-wave ($$\ell=0$$, $$\lambda = \nu$$) gives
$$\tan\delta_0 = J_\nu(ka)/N_\nu(ka)$$. For $$d=3$$, this yields the exact
$$\delta_0 = -ka$$, $$a_{\mathrm{sc}} = a$$, and $$\sigma_{\mathrm{tot}} \to 4\pi a^2$$ —
four times the classical geometric cross section, a quantum diffraction effect.

---

### 10 Finite Spherical Well: $$V(r) = -V_0$$ for $$r < a$$

In the interior, the radial equation becomes the free equation with
$$k \to K = \sqrt{k^2 + 2mV_0/\hbar^2}$$. The regular solution is

$$
u_\ell^{\mathrm{in}}(r) = B\sqrt{Kr}\,J_\lambda(Kr).
$$

Continuity of $$u_\ell$$ and $$u_\ell'$$ at $$r = a$$ gives

$$
\tan\delta_\ell = \frac{k\,[\sqrt{\rho}\,J_\lambda]'\big|_{ka}\,J_\lambda(Ka) - K\,[\sqrt{\rho}\,J_\lambda]'\big|_{Ka}\,J_\lambda(ka)}{k\,[\sqrt{\rho}\,N_\lambda]'\big|_{ka}\,J_\lambda(Ka) - K\,[\sqrt{\rho}\,J_\lambda]'\big|_{Ka}\,N_\lambda(ka)}.
$$

When $$\delta_\ell$$ passes through $$\pi/2$$ (mod $$\pi$$), $$\sin^2\!\delta_\ell = 1$$
(unitarity limit). Near a resonance at $$E_r$$ with width $$\Gamma$$:

\begin{equation}\label{eq.breit.wigner}
\sigma_\ell \propto \frac{(\Gamma/2)^2}{(E-E_r)^2 + (\Gamma/2)^2} \qquad \text{(Breit–Wigner)},
\end{equation}

physically corresponding to temporary trapping with lifetime $$\tau = \hbar/\Gamma$$. The
s-wave scattering length diverges ($$a_d \to \pm\infty$$) precisely when the potential is
on the verge of supporting a new bound state — a deep and universal connection.

---

### 11 Born Approximation and the Yukawa Potential

#### 11.1 The Born approximation

When the potential is weak or the energy is high, the wave function inside the interaction
region is approximately the incident plane wave itself. Substituting
$$\psi(\mathbf{r}')$$ by $$\mathrm{e}^{\mathrm{i}\mathbf{k}\cdot\mathbf{r}'}$$ in the
exact integral expression for $$f$$:

$$
f^{(1)}(\theta) \propto -\frac{2m}{\hbar^2}\int \mathrm{d}^d r'\,\mathrm{e}^{-\mathrm{i}\mathbf{q}\cdot\mathbf{r}'}\,V(r'), \qquad \mathbf{q} = \mathbf{k}' - \mathbf{k}, \quad q = 2k\sin\frac{\theta}{2}.
$$

For a central potential, the angular integration gives

$$
f^{(1)}(\theta) \propto -\frac{2m}{\hbar^2}\int_0^\infty r'^{d-2}\,V(r')\frac{J_\nu(qr')}{(qr')^\nu}\,\mathrm{d}r'.
$$

The angular integral is the $$\ell=0$$ case of the Rayleigh expansion \eqref{eq.rayleigh}:
all other contributions vanish by Gegenbauer orthogonality. The Born approximation is
accurate when $$|V| \ll E$$ or $$|V| \ll \hbar^2/(ma^2)$$.

#### 11.2 The Yukawa potential

**Definition** (Yukawa potential in $$d$$ dimensions).

\begin{equation}\label{eq.yukawa}
V(r) = V_0\,\frac{\mathrm{e}^{-\mu r}}{r},
\end{equation}

with $$V_0$$ the coupling constant and $$\mu > 0$$ the inverse range. The definition is a
radial function; it has the same functional form in every dimension. The Yukawa potential
satisfies all the standing assumptions in every $$d$$. It describes the interaction
mediated by massive bosons: pion exchange between nucleons ($$1/\mu \approx 1.4\,\mathrm{fm}$$),
screened Coulomb in plasmas (with $$1/\mu$$ the Debye length), and the weak force at low
energies.

#### 11.3 Born amplitude in $$d$$ dimensions

Substituting \eqref{eq.yukawa} into the Born formula:

$$
f^{(1)}(\theta) \propto -\frac{2mV_0}{\hbar^2}\int_0^\infty r'^{d-2}\,\mathrm{e}^{-\mu r'}\frac{J_\nu(qr')}{(qr')^\nu}\,\mathrm{d}r'.
$$

For general $$d$$ the integral is not elementary (it can be written in terms of
$$_2F_1$$), but the physical content is clear: the Born amplitude is the $$d$$-dimensional
Fourier transform of a short-range potential and decays as $$q$$ increases. The
exponential cut-off $$\mathrm{e}^{-\mu r}$$ ensures convergence in every $$d$$.

#### 11.4 Specialisation to $$d=3$$

For $$d=3$$, $$\nu = \tfrac{1}{2}$$, and $$J_{1/2}(z)/z^{1/2} = \sqrt{2/\pi}\sin(z)/z$$. Substituting:

$$
f^{(1)}(\theta) = -\frac{2mV_0}{\hbar^2}\int_0^\infty \mathrm{e}^{-\mu r'}\frac{\sin(qr')}{q}\,\mathrm{d}r' \qquad [d=3].
$$

The integral is elementary. Writing $$\sin(qr') = (\mathrm{e}^{\mathrm{i}qr'} - \mathrm{e}^{-\mathrm{i}qr'})/(2\mathrm{i})$$:

$$
\int_0^\infty \mathrm{e}^{-\mu r'}\sin(qr')\,\mathrm{d}r' = \frac{q}{\mu^2+q^2},
$$

hence the final result in $$d=3$$:

\begin{equation}\label{eq.yukawa.born.3d}
f^{(1)}(\theta) = -\frac{2mV_0}{\hbar^2}\cdot\frac{1}{q^2+\mu^2} = -\frac{2mV_0/\hbar^2}{\mu^2 + 4k^2\sin^2(\theta/2)} \qquad [d=3],
\end{equation}

with differential cross section

$$
\frac{\mathrm{d}\sigma}{\mathrm{d}\Omega} = |f^{(1)}(\theta)|^2 = \left(\frac{2mV_0}{\hbar^2}\right)^2\frac{1}{[\mu^2 + 4k^2\sin^2(\theta/2)]^2} \qquad [d=3].
$$

#### 11.5 Three important limits

**Coulomb limit: $$\mu \to 0$$.** Taking $$\mu\to 0$$ with $$V_0 \equiv \alpha$$ (so that
$$V(r)\to\alpha/r$$):

\begin{equation}\label{eq.rutherford}
\frac{\mathrm{d}\sigma}{\mathrm{d}\Omega} \xrightarrow{\mu\to 0} \left(\frac{\alpha}{4E}\right)^2\frac{1}{\sin^4(\theta/2)}.
\end{equation}

This is the **Rutherford formula**! The Born approximation for the Yukawa potential, in
the zero-mass limit of the mediator, reproduces the exact Coulomb cross section.
Remarkably, the Rutherford formula is identical in three distinct treatments: classical
(Rutherford, 1911), Born (above), and exact quantum (via separation in parabolic
coordinates). This agreement is specific to the $$1/r$$ potential and is related to its
hidden $$SO(4)$$ symmetry — the same one that gives the accidental degeneracy of hydrogen.

**Low-energy limit: $$k\to 0$$.** For $$k\ll\mu$$, $$f^{(1)} \to -2mV_0/(\hbar^2\mu^2) \equiv -a_Y$$,
isotropic. Identifying $$-a_Y$$ with the scattering length:

$$
a_Y^{(\mathrm{Born})} = \frac{2mV_0}{\hbar^2\mu^2},
$$

and $$\sigma_{\mathrm{tot}} \to 4\pi a_Y^2$$.

**High-energy limit: $$k\gg\mu$$.** For $$q\gg\mu$$, $$\mu^2$$ is negligible compared
with $$q^2$$:

$$
\frac{\mathrm{d}\sigma}{\mathrm{d}\Omega} \xrightarrow{k\gg\mu} \left(\frac{2mV_0}{\hbar^2}\right)^2\frac{1}{q^4},
$$

the screened Rutherford formula: at high energies, the particle probes distances much
smaller than $$1/\mu$$ and sees an effective $$1/r$$.

#### 11.6 An additional remark on the electrostatic Yukawa

The potential \eqref{eq.yukawa} retains the same functional form $$\mathrm{e}^{-\mu r}/r$$
in every $$d$$. A different generalisation, physically motivated, is the screened Poisson
Green's function $$G_\mu^{(d)}(r) \propto (\mu/r)^\nu K_\nu(\mu r)$$, the solution of
$$(-\nabla_d^2 + \mu^2)G = \delta^{(d)}(\mathbf{r})$$, whose $$d$$-dimensional Fourier
transform is $$1/(q^2+\mu^2)$$ in every $$d$$. For $$d=3$$,
$$K_{1/2}(z) = \sqrt{\pi/(2z)}\,\mathrm{e}^{-z}$$ and $$G_\mu^{(3)} \propto \mathrm{e}^{-\mu r}/r$$ — the
usual Yukawa. For $$d\neq 3$$ the two generalisations differ.

---

### 12 Coulomb-type Potentials

There are two natural candidates for the "Coulomb potential" in $$d$$ dimensions, and
they differ for $$d\neq 3$$. We treat each separately.

**Option A** is $$V(r) = -\alpha/r$$ in every $$d$$. This is not the electrostatic
potential of a point charge for $$d\neq 3$$, but has the special mathematical property
that the radial equation reduces to the confluent hypergeometric equation in every $$d$$.

**Option B** is $$V(r) = -\alpha/r^{d-2}$$. This is the genuine electrostatic potential
in $$d$$ dimensions (the Green's function of $$\nabla_d^2$$). But for $$d\neq 3$$ it does
not reduce to a standard special-function equation.

To see why the electrostatic potential is $$1/r^{d-2}$$, one applies Gauss's law in
$$d$$ dimensions: $$E(r)\cdot\Omega_d r^{d-1} = \text{const}$$, hence $$E(r)\propto 1/r^{d-1}$$.
Integrating $$V = -\int E\,\mathrm{d}r$$ gives $$V(r)\propto 1/r^{d-2}$$. For $$d=3$$ this
is $$1/r$$; for $$d=4$$ it is $$1/r^2$$; for $$d=2$$ it is $$\ln r$$.

#### 12.1 Option A: $$V = -\alpha/r$$ — the confluent hypergeometric equation

For $$V(r) = -\alpha/r$$, the radial equation becomes

$$
u_\ell'' + \left[k^2 + \frac{2\eta k}{r} - \frac{\lambda^2-\frac{1}{4}}{r^2}\right]u_\ell = 0, \qquad \eta = \frac{m\alpha}{\hbar^2 k},
$$

with $$\eta$$ the **Sommerfeld parameter**. The substitution $$\rho = -2\mathrm{i}kr$$
transforms it into the **confluent hypergeometric equation**

$$
\rho\,w'' + (b-\rho)\,w' - a\,w = 0,
$$

with $$a = \lambda + \tfrac{1}{2} + \mathrm{i}\eta = \ell + (d-1)/2 + \mathrm{i}\eta$$ and
$$b = 2\lambda+1 = 2\ell+d-1$$. The regular solution is

\begin{equation}\label{eq.coulomb.regular}
u_\ell(r) = C\,(2kr)^{\lambda+1/2}\,\mathrm{e}^{\mathrm{i}kr}\;{}_1F_1\!\left(\lambda+\tfrac{1}{2}+\mathrm{i}\eta;\;2\lambda+1;\;-2\mathrm{i}kr\right).
\end{equation}

This is the same $${}_1F_1$$ that appears in the bound states of the hydrogen atom.

The asymptotic expansion for large $$|z|$$ of $${}_1F_1(a;b;z)$$ gives

$$
{}_1F_1(a;b;z) \sim \frac{\Gamma(b)}{\Gamma(b-a)}(-z)^{-a} + \frac{\Gamma(b)}{\Gamma(a)}\mathrm{e}^z z^{a-b}.
$$

For $$z = -2\mathrm{i}kr$$, these terms oscillate as $$\mathrm{e}^{\mp\mathrm{i}kr}$$ (incoming
and outgoing waves). The ratio of outgoing to incoming amplitudes gives the
$$S$$-matrix element. Since $$|\Gamma(\alpha+\mathrm{i}\beta)| = |\Gamma(\alpha-\mathrm{i}\beta)|$$,
this ratio has unit modulus (unitarity), and its phase gives

\begin{equation}\label{eq.coulomb.phase}
S_\ell^C = \mathrm{e}^{2\mathrm{i}\sigma_\ell^C}, \qquad \sigma_\ell^C = \arg\Gamma\!\left(\lambda+\tfrac{1}{2}+\mathrm{i}\eta\right).
\end{equation}

In $$d=3$$, the exact amplitude can be obtained from the separation in parabolic
coordinates:

$$
f_C(\theta) = -\frac{\eta}{2k\sin^2(\theta/2)}\exp\!\left[-\mathrm{i}\eta\ln\sin^2\frac{\theta}{2} + 2\mathrm{i}\sigma_0\right],
$$

giving the Rutherford cross section $$\mathrm{d}\sigma/\mathrm{d}\Omega = \eta^2/[4k^2\sin^4(\theta/2)]$$.
The $$1/r$$ tail modifies the asymptotic wave function at all distances, producing a
logarithmic phase that prevents pointwise convergence of the partial-wave series; the sum
requires Sommerfeld regularisation.

#### 12.2 Option B: $$V = -\alpha/r^{d-2}$$ — the genuine electrostatic potential

For the genuine $$d$$-dimensional Coulomb potential, the radial equation is

$$
u_\ell'' + \left[k^2 - \frac{\tilde{\alpha}}{r^{d-2}} - \frac{\lambda^2-\frac{1}{4}}{r^2}\right]u_\ell = 0, \qquad \tilde{\alpha} = \frac{2m\alpha}{\hbar^2}.
$$

For $$d=3$$ we recover the previous case. For $$d\neq 3$$ the structure changes
qualitatively: in $$d=2$$, $$V\propto\ln r$$ (logarithmic); in $$d=4$$, $$V\propto 1/r^2$$,
merging with the centrifugal barrier and producing pathologies (fall to the centre,
conformal symmetry); in $$d=5$$, $$V\propto 1/r^3$$; in general, with no closed-form
solution in standard special functions. The Born approximation for $$V=-\alpha/r^{d-2}$$
works in every $$d$$ and generalises Rutherford, since the Fourier transform of
$$1/r^{d-2}$$ in $$d$$ dimensions is $$1/q^2$$ (up to a constant).

---

### 13 Summary

The central points of the document can be summarised as follows.

**Structure.** The $$d$$-dimensional problem of scattering by a central potential
separates into a universal angular equation (valid for every $$V$$) and a
potential-specific radial equation. The angular one has eigenvalue $$\ell(\ell+d-2)$$
and eigenfunctions in hyperspherical form involving Gegenbauer polynomials $$C_\ell^\nu$$
with $$\nu = (d-2)/2$$. The radial one reduces to an effective 1D problem via
$$R = u/r^{(d-1)/2}$$, with effective angular momentum $$\mathcal{L} = \ell + (d-3)/2$$.

**Procedure.** Given $$V(r)$$: (i) solve the radial equation in the interior; (ii) compute
the logarithmic derivative $$\gamma_\ell$$ at $$R_0$$; (iii) match with the exterior
solution to obtain $$\delta_\ell$$; (iv) sum the partial-wave expansion to get $$f(\theta)$$;
(v) the cross section is $$|f|^2$$, and at low energy one extracts the scattering length
$$a_d$$.

**Substitution rule $$d=3\to d$$.** 
$$\ell(\ell+1)\to\ell(\ell+d-2)$$, 
$$j_\ell,n_\ell \to J_{\ell+\nu},N_{\ell+\nu}$$, 
$$P_\ell \to C_\ell^\nu$$, 
$$r^{-1}\to r^{-(d-1)/2}$$.

**Examples.** The hard sphere in $$d=3$$ gives $$\sigma_{\mathrm{tot}}\to 4\pi a^2$$ at
low energy (four times the classical value). The spherical well exhibits Breit–Wigner-type
resonances. The Born approximation applied to the Yukawa potential gives
$$f^{(1)}\propto -1/(q^2+\mu^2)$$ in $$d=3$$ and, in the limit $$\mu\to 0$$, recovers
Rutherford.

**Pathological case of Coulomb.** The $$1/r$$ potential has infinite range, violates
the short-range hypothesis, and requires separate treatment — with Coulomb wave functions
and separation in parabolic coordinates. Apart from this, Option A ($$1/r$$ in every
$$d$$) reduces to the confluent hypergeometric equation, the same one as for hydrogen:
bound states ($$E < 0$$) and scattering ($$E > 0$$) are two faces of the same mathematical
problem.

---

### 14 The Complete Scattering Procedure

The complete procedure, from a given potential $$V(r)$$ to all observables, is summarised
by the chain:

$$
V(r)\;\xrightarrow[\text{solve radial eq.}]{\text{interior}}\;\gamma_\ell \;\xrightarrow[\text{Eq.\eqref{eq.tan.delta}}]{\text{matching at }R_0}\;\delta_\ell(k)\;\xrightarrow[\text{Eq.\eqref{eq.f.theta}}]{\text{Gegenbauer sum}}\;f(\theta)\;\xrightarrow{|f|^2}\;\frac{\mathrm{d}\sigma}{\mathrm{d}\Omega}\;\xrightarrow{k\to 0}\;a_d.
$$
