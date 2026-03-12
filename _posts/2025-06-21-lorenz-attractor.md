---
layout: page
title: Chaos and the Lorenz Attractor
date: 2025-06-21 11:00:00-0400
description: Deterministic chaos, sensitive dependence on initial conditions, strange attractors, and Lyapunov exponents
tags: math physics chaos
categories: fun
related_posts: false
---

In 1963, Edward Lorenz discovered that a simple system of three ordinary differential equations — a drastically simplified model of atmospheric convection — could produce utterly unpredictable behaviour. This was the birth of modern **chaos theory**.

### The Lorenz equations

The Lorenz system is

\begin{equation}\label{eq.lorenz}
\dot{x} = \sigma(y - x), \qquad
\dot{y} = x(\rho - z) - y, \qquad
\dot{z} = xy - \beta z,
\end{equation}

where the standard parameter values are $$\sigma = 10$$ (Prandtl number), $$\rho = 28$$ (Rayleigh number ratio), and $$\beta = 8/3$$ (geometric factor). These values place the system firmly in the **chaotic regime**.

The variables $$x, y, z$$ represent, loosely: the intensity of convective motion ($$x$$), the temperature difference between rising and falling fluid ($$y$$), and the departure of the temperature profile from linearity ($$z$$).

### Fixed points and their instability

Setting $$\dot{x} = \dot{y} = \dot{z} = 0$$, the fixed points for $$\rho > 1$$ are

\begin{equation}
C_0 = (0,0,0), \quad C_\pm = \bigl(\pm\sqrt{\beta(\rho-1)},\,\pm\sqrt{\beta(\rho-1)},\, \rho-1\bigr).
\end{equation}

For $$\rho = 28$$: $$C_\pm = (\pm 6\sqrt{2}, \pm 6\sqrt{2}, 27)$$. The Jacobian at $$C_\pm$$ has eigenvalues with positive real part, so **all three fixed points are unstable**. The trajectory cannot settle — it is perpetually repelled from every equilibrium, yet bounded.

### The strange attractor

Although the Lorenz system is dissipative (the volume in phase space contracts at rate $$\dot{V}/V = -(\sigma + 1 + \beta) = -41/3$$), the attractor is neither a point nor a limit cycle nor a torus. It has **non-integer (fractal) dimension** $$d \approx 2.06$$. This is a **strange attractor**.

The trajectory winds around $$C_+$$, spirals outward, falls toward $$C_-$$, winds around it, spirals outward again, and switches unpredictably between the two lobes — the famous **butterfly shape**.

### Sensitive dependence on initial conditions

Two trajectories starting at distance $$\delta_0$$ apart diverge (on average) as

\begin{equation}
\delta(t) \approx \delta_0\, e^{\lambda_1 t},
\end{equation}

where $$\lambda_1 \approx 0.906$$ is the **maximal Lyapunov exponent** of the Lorenz system. Positive $$\lambda_1$$ is the mathematical definition of chaos: nearby trajectories diverge exponentially. After time $$T \approx \ln(\Delta/\delta_0)/\lambda_1$$ (where $$\Delta$$ is the attractor size), all predictability is lost.

For $$\delta_0 \sim 10^{-6}$$ and $$\Delta \sim 30$$: $$T \approx 17$$ Lorenz time units. In the atmospheric analogy, doubling $$\delta_0$$ buys only $$\ln 2/\lambda_1 \approx 0.76$$ extra time units of forecast — the root of the **two-week weather prediction barrier**.

### The Lorenz map

A remarkable feature: plot the $$n$$-th local maximum of $$z(t)$$, call it $$z_n$$, against the next maximum $$z_{n+1}$$. The result is a **one-dimensional tent map**:

\begin{equation}
z_{n+1} \approx f(z_n),
\end{equation}

where $$f$$ is approximately piecewise-linear with slope $$|f'| > 1$$. This one-dimensional return map captures essentially all of the chaotic dynamics and explains why the Lorenz system is rigorously chaotic (it is conjugate to a shift on a symbolic sequence).

### Lyapunov spectrum

The full Lyapunov spectrum $$(\lambda_1, \lambda_2, \lambda_3)$$ of the Lorenz system satisfies:

- $$\lambda_1 \approx +0.906$$ (divergence — chaos)
- $$\lambda_2 = 0$$ (along the flow)
- $$\lambda_3 \approx -14.572$$ (strong contraction)

The **Kaplan–Yorke dimension** is

\begin{equation}
d_{\rm KY} = 2 + \frac{\lambda_1 + \lambda_2}{|\lambda_3|} \approx 2 + \frac{0.906}{14.572} \approx 2.062,
\end{equation}

confirming the fractal nature of the attractor.

### Simulation and visualisation

The following Python code integrates the Lorenz system with a simple Runge–Kutta 4 scheme and plots the butterfly attractor:

```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

def lorenz(state, sigma=10, rho=28, beta=8/3):
    x, y, z = state
    return np.array([
        sigma * (y - x),
        x * (rho - z) - y,
        x * y - beta * z
    ])

def rk4(f, state, dt):
    k1 = f(state)
    k2 = f(state + 0.5*dt*k1)
    k3 = f(state + 0.5*dt*k2)
    k4 = f(state + dt*k3)
    return state + (dt/6) * (k1 + 2*k2 + 2*k3 + k4)

dt = 0.01
n_steps = 10_000
state = np.array([0.1, 0.0, 0.0])
traj = np.zeros((n_steps, 3))
for i in range(n_steps):
    state = rk4(lorenz, state, dt)
    traj[i] = state

fig = plt.figure(figsize=(8, 6))
ax = fig.add_subplot(111, projection='3d')
ax.plot(traj[:, 0], traj[:, 1], traj[:, 2],
        lw=0.4, alpha=0.8, color='steelblue')
ax.set_xlabel('x'); ax.set_ylabel('y'); ax.set_zlabel('z')
ax.set_title('Lorenz Attractor  ($\\sigma=10,\\,\\rho=28,\\,\\beta=8/3$)')
plt.tight_layout(); plt.savefig('lorenz_attractor.png', dpi=150); plt.show()
```

**Sensitive dependence visualisation** — two trajectories separated by $$\delta_0 = 10^{-8}$$:

```python
dt = 0.01
s1 = np.array([0.1, 0.0, 0.0])
s2 = s1 + np.array([1e-8, 0, 0])

times, dists = [], []
for t in np.arange(0, 50, dt):
    s1 = rk4(lorenz, s1, dt)
    s2 = rk4(lorenz, s2, dt)
    times.append(t)
    dists.append(np.linalg.norm(s2 - s1))

plt.semilogy(times, dists, lw=0.8)
plt.axhline(1e-8, ls='--', color='gray', label=r'$\delta_0$')
t_arr = np.array(times)
plt.semilogy(t_arr, 1e-8 * np.exp(0.906 * t_arr), 'r--',
             label=r'$\delta_0 e^{\lambda_1 t}$')
plt.xlabel('Time'); plt.ylabel(r'$\|\delta(t)\|$')
plt.legend(); plt.tight_layout(); plt.show()
```

The exponential divergence (red dashed line) matches perfectly until the two trajectories are saturated by the attractor size at $$t \approx 30$$.

### Beyond the Lorenz system

The Lorenz system belongs to a wider zoo of chaotic systems. Related landmarks:

- **Rössler attractor** (1976) — simpler equations, single spiral lobe
- **Double pendulum** — chaotic with only two degrees of freedom
- **Hénon map** — discrete-time analogue with fractal basin boundaries
- **KAM theory** — coexistence of regular (quasi-periodic) and chaotic orbits in Hamiltonian systems; chaos spreads from hyperbolic fixed points as energy increases (Chirikov criterion)

The universality of chaos is captured by **Feigenbaum's constants**: the period-doubling route to chaos (e.g., in the logistic map $$x_{n+1} = rx_n(1-x_n)$$) is governed by the ratio $$\delta = 4.669...$$ between successive bifurcation intervals, independent of the particular map.
