---
layout: page
title: "Newton vs Einstein in the solar system: a simulator"
date: 2026-10-18 12:00:00-0300
description: A Python solar-system simulator that integrates the planets with Newtonian gravity and then with General Relativity, and measures the difference — Mercury's famous 43 arcseconds per century come out of the simulation itself, together with the planets' 530", light bending, the Shapiro delay, and the small effects that compete with GR
img:
tags: physics gravity relativity simulation python
categories: fun
related_posts: false
---

In 1859 Urbain Le Verrier, fresh from predicting Neptune out of Uranus' misbehaviour, reported
that Mercury's perihelion was drifting about 38 arcseconds per century faster than the known
planets could explain (Newcomb later refined this to 43"). A planet inside Mercury's orbit,
Vulcan, was proposed, hunted for, and even "seen" a few times, but it never existed. In November
1915 Einstein computed the perihelion shift implied by his brand-new field equations and found
43" per century. He wrote that for a few days he was "beside myself with joyous excitement".

That number is one of the great tests of General Relativity, and it is small enough to be
delicate and large enough to be reproducible on a laptop. So I built
[gravsim](https://github.com/ftahas/gravsim): a Python package, nine lesson notebooks, a Streamlit
lab and a 3-D web viewer that integrate the solar system first with Newton, then with Einstein,
and make the difference *measurable*. This post walks through the physics and shows what comes out.

<div class="row justify-content-sm-center">
    <div class="col-sm-12 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/gravsim/viewer_inner_3d.png" title="gravsim 3-D viewer: inner solar system, Newton vs GR" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    The 3-D viewer (Three.js in the browser, physics in Python) 70 years into a century-long run.
    Both the Newtonian and the relativistic orbits are drawn; the GR − Newton displacement is
    amplified about 2000× so that the arc of Mercury's perihelion markers, otherwise invisible, shows the
    relativistic advance running ahead of the Newtonian one.
</div>

---

### Newton first: the clockwork solar system

The Newtonian problem is nine point masses pulling on each other,

\begin{equation}\label{eq.newton}
\ddot{\mathbf{r}}_i = -\sum_{j\neq i} \frac{G m_j\,(\mathbf{r}_i-\mathbf{r}_j)}{|\mathbf{r}_i-\mathbf{r}_j|^3},
\end{equation}

started from the real state of the Sun and the eight planets at J2000.0, taken from the JPL
Horizons ephemeris. Everything is done in astronomical units, days and $$GM$$ values (DE440), in
the barycentric J2000 ecliptic frame, so the Sun moves too: Jupiter drags it around the
barycentre by about 1.6 solar radii.

<div class="row justify-content-sm-center">
    <div class="col-sm-12 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/gravsim/solar_system_3d.png" title="Sun + 8 planets, 100 years, Newtonian" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    A century of Newtonian motion for the Sun and eight planets (left) and the inner planets (right),
    integrated with an 8th-order Dormand–Prince scheme at relative tolerance $$10^{-12}$$.
</div>

Before claiming anything about relativity one has to be sure the numerics are not inventing a
drift. The relativistic signal we are after is $$5\times10^{-7}$$ radians per orbit of Mercury,
a tenth of an arcsecond, and a fixed-step integrator produces a *spurious* perihelion precession
of order $$(2\pi/N)^2$$ per orbit for $$N$$ steps per orbit. With half-day steps, plain leapfrog
"discovers" a precession of $$-2\times10^{5}$$ arcseconds per century, four thousand times the
effect we want to measure. The package therefore implements the usual ladder of integrators
(Euler, symplectic Euler, leapfrog, RK4, Yoshida 4th and 6th order) as teaching material, and uses
the adaptive DOP853 scheme for production runs, where the numerical precession of a two-body
Kepler orbit over a century comes out at 0.001" per century. That is the noise floor.

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/gravsim/energy_error.png" title="Relative energy error of the integrators" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Relative energy error over time. Symplectic schemes keep it bounded; Runge–Kutta drifts; the
    adaptive 8th-order scheme stays at the $$10^{-13}$$ level for a century.
</div>

### Measuring a drift of 0.1 arcsecond per orbit

The instrument is the Laplace–Runge–Lenz (eccentricity) vector, which points at perihelion and is
conserved exactly in the Kepler problem:

\begin{equation}\label{eq.lrl}
\mathbf{e} = \frac{\mathbf{v}\times\mathbf{h}}{GM} - \frac{\mathbf{r}}{r}, \qquad \mathbf{h}=\mathbf{r}\times\mathbf{v}.
\end{equation}

Its direction, expressed as the longitude of perihelion $$\varpi$$, is computed at every sample of
the run; a least-squares slope of $$\varpi(t)$$ gives the precession rate. In the full N-body run
$$\varpi$$ wobbles by tens of arcseconds under the periodic pull of Venus and Jupiter, and the
secular rate from the planets alone is Le Verrier's 530" per century. The relativistic 43" sits on
top of that, which is why the cleanest measurement is a *difference*: run the same initial state
with and without the relativistic term, on the same time grid, and subtract the two $$\varpi(t)$$
series. The planetary wobble and the integrator error cancel almost perfectly and the GR advance
is left as a straight line.

<div class="row justify-content-sm-center">
    <div class="col-sm-12 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/gravsim/mercury_perihelion_newton_vs_gr.png" title="Mercury's longitude of perihelion, Newton vs Newton + 1PN" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Left: Mercury's osculating longitude of perihelion over a century in a Sun + 8 planet run,
    with and without the relativistic correction; the planets dominate. Right: the difference of the
    two runs. The slope is 42.98 ± 0.001 arcseconds per century.
</div>

### From Einstein's equations to the 43 arcseconds

Before the force law that the code integrates, here is where that law comes from, because the
whole point of the project is that the number is *derived*, not fitted. The chain is: field
equations → the metric outside the Sun → the geodesic equation → an orbit equation that is
Newton's plus one term → the precession.

**The field equations.** General Relativity replaces the gravitational potential by the metric
$$g_{\mu\nu}$$ of spacetime and Poisson's equation by Einstein's field equations,

\begin{equation}\label{eq.efe}
R_{\mu\nu} - \tfrac{1}{2} R\, g_{\mu\nu} = \frac{8\pi G}{c^4}\, T_{\mu\nu},
\end{equation}

where the Ricci tensor $$R_{\mu\nu}$$ and the scalar $$R = g^{\mu\nu}R_{\mu\nu}$$ are built from
second derivatives of the metric, and $$T_{\mu\nu}$$ is the energy–momentum of matter. Outside the
Sun $$T_{\mu\nu} = 0$$, and taking the trace of \eqref{eq.efe} gives $$R = 0$$, so the vacuum
equations are simply $$R_{\mu\nu} = 0$$: ten coupled nonlinear partial differential equations for
the ten components of $$g_{\mu\nu}$$. Matter still enters, through the boundary condition that
far from the Sun the field must reduce to Newton's: comparing the geodesic equation below with
Newton's second law in the weak-field, slow-motion limit forces
$$g_{00} \to -(1 + 2\Phi/c^2)$$ with $$\Phi = -GM/r$$. That identification is also what fixes
the constant $$8\pi G/c^4$$ in front of $$T_{\mu\nu}$$.

**The Schwarzschild solution.** For a static, spherically symmetric source the vacuum equations
have a unique solution, found by Karl Schwarzschild within weeks of Einstein's paper
(and, by Birkhoff's theorem, the only one even if the star pulsates radially):

\begin{equation}\label{eq.schw}
ds^2 = -\left(1-\frac{r_s}{r}\right)c^2\,dt^2 + \left(1-\frac{r_s}{r}\right)^{-1} dr^2 + r^2\left(d\theta^2 + \sin^2\theta\, d\phi^2\right),
\qquad r_s = \frac{2GM}{c^2}.
\end{equation}

For the Sun $$r_s = 2.95$$ km, and at Mercury's orbit $$r_s/r \approx 5\times10^{-8}$$. That ratio
is the size of everything relativistic in the inner solar system, and it is why the effect took
until 1859 to notice and until 1915 to explain.

**Geodesics.** A planet is a test body, so it follows a geodesic of \eqref{eq.schw}: it
extremises the proper time $$\tau$$ along its path. The equations of motion come from the
Lagrangian $$\mathcal{L} = \tfrac{1}{2} g_{\mu\nu}\dot{x}^\mu \dot{x}^\nu$$ with
$$\dot{\ } = d/d\tau$$. Two coordinates are cyclic, so two quantities are conserved along the
orbit, and spherical symmetry lets us put the orbit in the plane $$\theta = \pi/2$$:

\begin{equation}\label{eq.geo}
E = \left(1-\frac{r_s}{r}\right) c^2\, \dot t, \qquad L = r^2 \dot\phi .
\end{equation}

$$E$$ is the energy per unit mass including rest energy, $$L$$ the angular momentum per unit mass:
Kepler's second law survives intact, only with proper time as the clock. The third equation is
the normalisation $$g_{\mu\nu}\dot x^\mu \dot x^\nu = -c^2$$ of the four-velocity, which with
\eqref{eq.geo} becomes a radial energy equation,

\begin{equation}\label{eq.veff}
\tfrac{1}{2}\dot r^2 + V_{\rm eff}(r) = \frac{E^2 - c^4}{2c^2},
\qquad
V_{\rm eff}(r) = -\frac{GM}{r} + \frac{L^2}{2r^2} - \frac{GM L^2}{c^2 r^3}.
\end{equation}

This is the whole of planetary motion in one line. The first two terms of $$V_{\rm eff}$$ are
exactly Newton's effective potential, gravity plus the centrifugal barrier; the third is the
relativistic correction. It is attractive, it falls off as $$1/r^3$$, and near a compact mass it
overwhelms the centrifugal barrier, which is where the innermost stable circular orbit and the
photon sphere come from (more on that below). Near the Sun it is a whisper: at Mercury's orbit
it is $$10^{-8}$$ of the Newtonian term. The simulation integrates \eqref{eq.veff} as it stands in
the "exact Schwarzschild" mode.

**The orbit equation.** Follow Binet: use $$u = 1/r$$ as the variable and $$\phi$$ as the
parameter. From \eqref{eq.geo}, $$\dot r = -L\, du/d\phi$$, so \eqref{eq.veff} becomes a first-order
equation in $$u(\phi)$$; differentiating it once with respect to $$\phi$$ gives

\begin{equation}\label{eq.binet}
\frac{d^2 u}{d\phi^2} + u = \frac{GM}{L^2} + \frac{3GM}{c^2}\, u^2 .
\end{equation}

Without the last term this is Newton's orbit equation, whose solution is the conic
$$u_0(\phi) = \frac{GM}{L^2}\left(1 + e\cos\phi\right)$$: a closed ellipse with the perihelion
fixed at $$\phi = 0$$ forever. The last term is all that General Relativity adds to the shape of
a planetary orbit, and it is small: writing it in terms of the Newtonian solution,

\begin{equation}\label{eq.epsilon}
\frac{3GM}{c^2}u_0^2 = \epsilon\,\frac{GM}{L^2}\left(1 + e\cos\phi\right)^2,
\qquad
\epsilon \equiv \frac{3\,(GM)^2}{c^2 L^2} = \frac{3GM}{c^2 a(1-e^2)} \approx 8\times10^{-8}
\end{equation}

for Mercury, where $$L^2 = GM a(1-e^2)$$ relates the angular momentum to the osculating ellipse.

**Perturbation theory.** Write $$u = u_0 + u_1$$ with $$u_1 = O(\epsilon)$$ and keep first
order. The correction obeys a driven harmonic oscillator,

\begin{equation}\label{eq.pert}
\frac{d^2 u_1}{d\phi^2} + u_1 = \epsilon\,\frac{GM}{L^2}\left(1 + 2e\cos\phi + e^2\cos^2\phi\right).
\end{equation}

The constant and the $$\cos^2\phi = \tfrac12(1+\cos 2\phi)$$ pieces on the right drive bounded,
periodic responses: they distort the ellipse by one part in $$10^{7}$$ and nothing accumulates.
The $$2e\cos\phi$$ piece is different: it drives the oscillator *at its own frequency*, which is
resonance, and the response grows without bound,

\begin{equation}\label{eq.secular}
u_1^{\rm (sec)} = \epsilon\,\frac{GM}{L^2}\; e\,\phi \sin\phi .
\end{equation}

Add it to $$u_0$$ and use $$\cos\phi + \epsilon\phi\sin\phi \approx \cos\big[(1-\epsilon)\phi\big]$$,
valid as long as $$\epsilon\phi \ll 1$$, that is for many thousands of orbits:

\begin{equation}\label{eq.orbit}
u(\phi) \approx \frac{GM}{L^2}\Big\{1 + e\cos\big[(1-\epsilon)\phi\big]\Big\}.
\end{equation}

The orbit is still an ellipse to this accuracy, but the angle has been rescaled: $$r$$ returns
to its minimum not after $$\phi = 2\pi$$ but after $$(1-\epsilon)\phi = 2\pi$$, so each
perihelion arrives $$2\pi/(1-\epsilon) - 2\pi \approx 2\pi\epsilon$$ later in angle than the last.
The ellipse turns, in the direction of motion, by

\begin{equation}\label{eq.advance}
\Delta\phi = 2\pi\epsilon = \frac{6\pi\,(GM)^2}{c^2 L^2} = \frac{6\pi G M}{c^2\, a\,(1-e^2)}
\end{equation}

per revolution. This is the formula Einstein wrote down on 18 November 1915. It depends on the
orbit only through $$a(1-e^2)$$, the semi-latus rectum, which is why Mercury, the closest and most
eccentric planet, is the one that shows it.

**The number.** For the Sun $$GM/c^2 = 1.4766$$ km; for Mercury $$a = 5.791\times10^{7}$$ km and
$$e = 0.2056$$, so $$a(1-e^2) = 5.546\times10^{7}$$ km and

\begin{equation}\label{eq.number}
\Delta\phi = 6\pi \times \frac{1.4766}{5.546\times10^{7}} = 5.02\times10^{-7}\ {\rm rad} = 0.1035''
\end{equation}

per orbit. Mercury completes $$36525/87.969 = 415.2$$ orbits per Julian century, which gives
$$42.98''$$ per century, Le Verrier's missing piece to two decimal places. The perturbative
treatment is accurate to relative order $$\epsilon$$ itself; the exact Schwarzschild advance,
which gravsim computes by integrating \eqref{eq.binet} numerically, differs from
\eqref{eq.advance} by $$10^{-4}$$ arcseconds per century, as the lesson on black-hole orbits checks.

**Where the force law comes from.** The N-body code cannot integrate a metric per body; it needs
an acceleration. Expanding the geodesic equation of a nearly-Newtonian metric in powers of
$$1/c^2$$ (the *post-Newtonian* expansion) gives the Newtonian acceleration plus a correction of
relative size $$v^2/c^2$$; the result in harmonic coordinates is equation \eqref{eq.pn1} below.
It contains the same physics as \eqref{eq.binet}, and indeed averaging it over a Kepler ellipse
reproduces \eqref{eq.advance} exactly. For several massive bodies the same expansion applied to
the full field equations, keeping every body as a source, gives the Einstein–Infeld–Hoffmann
equations that the ephemerides use.

### Einstein in the N-body code: the first post-Newtonian correction

In the weak-field, slow-motion limit the geodesic equation reduces to Newton's second law with
the Newtonian acceleration plus a correction of relative size
$$v^2/c^2 \sim GM/(c^2 r) \sim 10^{-8}$$ for Mercury. In harmonic coordinates, and with the
parametrised post-Newtonian (PPN) parameters $$\beta$$ and $$\gamma$$ left explicit (they measure,
respectively, the nonlinearity of gravity and the spatial curvature per unit mass; General
Relativity has $$\beta = \gamma = 1$$),

\begin{equation}\label{eq.pn1}
\mathbf{a}_{1\mathrm{PN}} = \frac{GM}{c^2 r^3}\left[\left(2(\beta+\gamma)\frac{GM}{r} - \gamma v^2\right)\mathbf{r} + 2(1+\gamma)(\mathbf{r}\cdot\mathbf{v})\,\mathbf{v}\right],
\end{equation}

which for GR ($$\beta=\gamma=1$$) is the familiar $$(4GM/r - v^2)\,\mathbf{r} + 4(\mathbf{r}\cdot\mathbf{v})\,\mathbf{v}$$.
Averaged over an orbit (Gauss's perturbation equations do the bookkeeping) this force turns the
ellipse by the PPN generalisation of \eqref{eq.advance},

\begin{equation}\label{eq.precession}
\Delta\varpi = \frac{2+2\gamma-\beta}{3}\,\frac{6\pi GM}{c^2 a(1-e^2)}
\end{equation}

per revolution. For Mercury the GR value is the 42.98" per century of \eqref{eq.number}; the
simulation, which knows nothing of the derivation above and only integrates \eqref{eq.pn1},
measures 42.98 ± 0.001. The same force applied to all planets gives 8.64" for Venus, 3.85" for the Earth and
1.35" for Mars (predicted 8.62, 3.84, 1.35), and plotting the measured advance per orbit against
$$a(1-e^2)$$ puts every planet on the $$1/(a(1-e^2))$$ line of equation \eqref{eq.precession}.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/gravsim/precession_vs_a.png" title="GR perihelion advance per orbit vs a(1−e²) for the planets" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Relativistic advance per orbit measured for each planet in the century-long N-body runs
    (GR minus Newton), against the analytic $$6\pi GM_\odot/(c^2 a(1-e^2))$$.
</div>

JPL does not use the test-particle formula: its ephemerides integrate the Einstein–Infeld–Hoffmann
equations, in which *every* body curves spacetime and the corrections involve all the mutual
potentials and velocities. gravsim implements those too (with $$\beta$$, $$\gamma$$). For Mercury
the EIH and the Sun-only correction differ by $$10^{-5}$$ arcseconds per century, and an independent
oracle, the REBOUNDx implementation of the same equations, agrees with gravsim's positions to 35
metres after ten years.

### Le Verrier's anomaly, from the data

The ephemeris can also play the role of the observations. Horizons includes relativity; a
Newtonian run started from the same state drifts away from it, and the drift is exactly the
missing term.

<div class="row justify-content-sm-center">
    <div class="col-sm-9 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/gravsim/mercury_vs_horizons.png" title="Mercury: distance from the Horizons ephemeris, Newton vs Newton + 1PN" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Mercury's distance from the JPL Horizons ephemeris over a century. The Newtonian run ends up
    5700 km away; with the relativistic term the residual is 180 km, most of it the unmodelled Moon
    and asteroids. Fitting Mercury's perihelion in the Horizons series itself and in the Newtonian run
    gives a difference of 43.0" per century: Le Verrier's anomaly, recovered from modern data.
</div>

### Seeing it: turn down the speed of light

At the true value of $$c$$ nothing is visible to the eye, so the lessons and the viewer have an
exaggeration knob. Scaling $$c$$ down by 100 multiplies the 1PN precession by $$10^4$$ while keeping
$$v/c \approx 0.02$$, so the expansion is still valid; Mercury's perihelion then advances about
0.3° per orbit and the ellipse visibly turns into a rosette. The measured rate stays within 0.2% of
equation \eqref{eq.precession} evaluated with the reduced $$c$$.

<div class="row justify-content-sm-center">
    <div class="col-sm-12 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/gravsim/exaggerated_c_rosette.png" title="Mercury with c/100: the rosette and the perihelion advance" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Left: every 20th of 200 orbits of Mercury with $$c/100$$; the ellipse turns by 57°. Right: the
    longitude of perihelion over 50 orbits and the analytic slope.
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm-12 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/gravsim/viewer_rosette.png" title="The rosette scenario in the 3-D viewer" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    The same scenario in the viewer, with the perihelion markers sweeping around the Sun.
</div>

### What if gravity were a different theory?

Because $$\beta$$ and $$\gamma$$ are explicit in the force laws, one can ask the simulator what a
different metric theory would do. Running the two-body problem with $$(\beta,\gamma)$$ equal to
$$(1,1)$$, $$(0,1)$$, $$(1,0)$$ and $$(2,1)$$ gives precession rates in the ratios
$$1 : 4/3 : 1/3 : 2/3$$, as the factor $$(2+2\gamma-\beta)/3$$ in equation \eqref{eq.precession}
requires, to four parts in $$10^4$$. Mercury alone constrains only this combination; the
degeneracy is broken by light, for which the deflection depends on $$(1+\gamma)/2$$ only, and it is
the Cassini measurement $$\gamma - 1 = (2.1\pm2.3)\times10^{-5}$$ that pins things down.

<div class="row justify-content-sm-center">
    <div class="col-sm-12 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/gravsim/ppn_precession_grid.png" title="Mercury's perihelion under four PPN parameter choices" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Mercury's perihelion advance relative to Newton for four choices of the PPN parameters, each
    against the prediction $$(2+2\gamma-\beta)/3 \times 42.98$$" per century.
</div>

### Beyond the expansion: exact Schwarzschild geodesics

The 1PN term is the first order of an expansion in $$GM/(c^2 r)$$, superb around the Sun
($$10^{-8}$$) and useless near a black hole. gravsim also integrates the exact timelike and null
geodesics of the Schwarzschild metric, that is, equations \eqref{eq.geo} and \eqref{eq.veff}
without any expansion. Everything follows from the effective potential of \eqref{eq.veff}, whose
$$-GML^2/(c^2 r^3)$$ term, a whisper at Mercury, becomes dominant at small $$r$$: it creates the innermost stable circular orbit at
$$6GM/c^2$$, the photon sphere at $$3GM/c^2$$, and orbits that whirl many times near periapsis before
zooming back out. For Mercury the exact geodesic advance agrees with the 1PN formula to
$$10^{-4}$$ arcseconds per century, which is the measure of how good the expansion is.

<div class="row justify-content-sm-center">
    <div class="col-sm-12 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/gravsim/viewer_black_hole.png" title="Zoom-whirl geodesic around a black hole" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    An exact Schwarzschild geodesic launched at $$r = 20\,GM/c^2$$ with periapsis at $$4.6\,GM/c^2$$,
    just outside the separatrix: the body whirls 2.8 times around the hole per radial period, an
    advance of 650° per orbit. The rings mark the horizon, the photon sphere and the ISCO.
</div>

### Light: Eddington 1919 and the Shapiro delay

Photons follow null geodesics, $$u'' + u = 3GM u^2/c^2$$ with $$u = 1/r$$, and a ray with impact
parameter $$b$$ is bent by

\begin{equation}\label{eq.deflection}
\delta = \frac{1+\gamma}{2}\,\frac{4GM}{c^2 b},
\end{equation}

twice Soldner's Newtonian corpuscle value of 1801 because space itself is curved
($$\gamma = 1$$). At the solar limb the exact geodesic gives 1.7512", the number Eddington's 1919
eclipse expedition set out to measure. The same geometry delays a radar signal grazing the Sun:
integrating the coordinate time along the null geodesic from the Earth to Mars at superior
conjunction gives a one-way Shapiro delay of 123.6 μs, within $$10^{-4}$$ of the weak-field formula
$$(1+\gamma)\,(GM/c^3)\ln\!\big[(r_e+r_r+R)/(r_e+r_r-R)\big]$$.

<div class="row justify-content-sm-center">
    <div class="col-sm-12 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/gravsim/light_bending_rays.png" title="Light rays past the Sun and deflection versus impact parameter" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Left: rays past the Sun with their deviation from straight exaggerated $$10^4$$ times. Right:
    deflection against impact parameter from the exact null geodesic, with Einstein's and Soldner's
    lines and the 1919 and modern VLBI measurements scaled to the limb.
</div>

### What else competes with GR?

Forty-three arcseconds is a difference between a measurement of 574" and a Newtonian prediction of
531", so one must know every other contribution at the 0.1" level. gravsim models the next three
and puts them on one chart.

<div class="row justify-content-sm-center">
    <div class="col-sm-9 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/gravsim/precession_budget.png" title="Mercury's perihelion budget" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Everything that moves Mercury's perihelion, measured in the simulation. The dotted line is the
    precision of a century of ranging.
</div>

* **The Sun's oblateness.** A quadrupole $$J_2 = 2.2\times10^{-7}$$ adds a $$1/r^4$$ force whose
  secular effect, by Kaula's formulas, is $$\tfrac32 n J_2 (R_\odot/p)^2 = 0.028$$" per century for
  Mercury; the run gives 0.0278. It has the same $$a$$-dependence structure as a change in $$\beta$$,
  which is why $$J_2$$ and $$\beta$$ were degenerate until Venus and MESSENGER ranging separated them.
* **Frame dragging.** The Sun's spin ($$J_\odot = 1.9\times10^{41}$$ kg m² s⁻¹) produces the
  Lense–Thirring acceleration $$\mathbf{a} = \frac{2G}{c^2 r^3}\big[\tfrac{3}{r^2}(\mathbf{r}\cdot\mathbf{J})\,\mathbf{r}\times\mathbf{v} + \mathbf{v}\times\mathbf{J}\big]$$,
  which drags the node forward and the perihelion backward: $$-0.002$$" per century for Mercury,
  measured as $$-0.0020$$. Amplifying $$J$$ by $$10^5$$ reproduces the analytic node and perigee
  rates to four decimal places.
* **The Moon.** Replacing the Earth–Moon barycentre by the Earth and the Moon changes Mercury's
  Newtonian rate by $$-0.0025$$" per century and leaves the relativistic difference untouched to
  $$10^{-7}$$. The Moon itself is a nice bonus: its perigee advances 40.6° per *year*, the largest
  "precession" in the solar system and purely Newtonian, driven by the Sun's tide, and its node
  regresses at 19.4°/yr, both matching the ephemeris over the same span to 0.01°/yr.

<div class="row justify-content-sm-center">
    <div class="col-sm-12 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/gravsim/moon_orbit.png" title="The Moon about the Earth and its perigee and node rates" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Left: two years of the Moon's orbit about the Earth with its perigees marked. Right: the
    longitudes of perigee and node over ten years with their secular fits.
</div>

### Running it

Everything is in the [gravsim repository](https://github.com/ftahas/gravsim): the package with
its own force laws, integrators and measurement toolkit (JPL Horizons and REBOUND are used only
as independent references), nine lesson notebooks that put the physics before the code, a seven-lab
Streamlit app, the 3-D viewer, theory pages with the derivations, and a validation script with 64
checks that reproduces every number quoted here.

```bash
git clone https://github.com/ftahas/gravsim && cd gravsim
scripts/setup_env.sh
.venv/bin/python scripts/validate.py      # the 64 checks, about two minutes
.venv/bin/gravsim-web --port 8000         # the 3-D viewer at http://localhost:8000
```

<div class="row justify-content-sm-center">
    <div class="col-sm-12 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/gravsim/viewer_earth_moon.png" title="Earth and Moon in the 3-D viewer" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    The viewer's Earth-following camera, with the Moon's orbit around the moving Earth.
</div>

It was built as a guided undergraduate project, and the thing I like most about it is that the
headline result is not a number copied from a textbook: integrate Newton, integrate Einstein,
subtract, and 42.98" per century is what you get.
