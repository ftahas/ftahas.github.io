---
layout: page
title: Black-Scholes equation
date: 2026-03-05 11:12:00-0400
description: Derivation and solution of the Black-Scholes equation for option pricing
img:
tags: math physics finance
categories: fun
related_posts: false
---

The Black-Scholes model is one of the most celebrated results in mathematical finance.
Published in 1973 by Fischer Black, Myron Scholes, and Robert Merton, it provides a
closed-form formula for pricing European options on a financial asset. Scholes and Merton
received the Nobel Prize in Economics in 1997 (Black had passed away in 1995).

### Financial options

A **European call option** is a contract that gives its holder the right — but not the
obligation — to buy an underlying asset at a fixed price $$K$$ (the *strike price*) at a
fixed future date $$T$$ (the *expiry*). Its payoff at expiry is

\begin{equation}
C(S_T, T) = \max(S_T - K,\, 0),
\end{equation}

where $$S_T$$ is the asset price at time $$T$$. A **European put option** gives the right
to *sell* at the strike, with terminal payoff

\begin{equation}
P(S_T, T) = \max(K - S_T,\, 0).
\end{equation}

The central question Black and Scholes answered is: **what is the fair price of these
contracts at any earlier time $$t < T$$?**

### The stochastic model: geometric Brownian motion

The fundamental assumption is that the asset price $$S_t$$ follows **geometric Brownian
motion** (GBM):

\begin{equation}\label{eq.gbm}
dS = \mu S\, dt + \sigma S\, dW_t,
\end{equation}

where $$\mu$$ is the *drift* (expected instantaneous return), $$\sigma > 0$$ is the
*volatility*, and $$W_t$$ is a standard Wiener process satisfying $$W_0 = 0$$ with
independent increments $$W_{t+\Delta t} - W_t \sim \mathcal{N}(0, \Delta t)$$.

The multiplicative structure ensures $$S_t > 0$$ for all $$t$$ and captures the
empirically observed fact that *returns* (not prices) are approximately normally
distributed. Equation \eqref{eq.gbm} can be solved exactly. Writing $$S = e^Y$$ and
applying the change of variables we find that $$Y_t = \ln S_t$$ follows *arithmetic*
Brownian motion:

\begin{equation}\label{eq.lognormal}
S_T = S_t \exp\!\left[\left(\mu - \tfrac{1}{2}\sigma^2\right)(T-t) + \sigma\sqrt{T-t}\, Z\right], \quad Z \sim \mathcal{N}(0,1).
\end{equation}

The correction $$-\tfrac{1}{2}\sigma^2$$ is the Ito correction arising from the
non-linearity of the logarithm when the driving noise is a Wiener process.

### Ito's lemma

Let $$V(S, t)$$ be the value of any derivative security written on $$S$$. Because $$S$$
is a stochastic process, ordinary calculus does not apply to $$V$$. The correct tool is
**Ito's lemma**: for any twice continuously differentiable function $$V(S,t)$$,

\begin{equation}\label{eq.ito}
dV = \frac{\partial V}{\partial t}\,dt + \frac{\partial V}{\partial S}\,dS
     + \frac{1}{2}\frac{\partial^2 V}{\partial S^2}(dS)^2.
\end{equation}

The crucial result from stochastic calculus is $$(dW_t)^2 = dt$$ (in the Ito sense), so
$$(dS)^2 = \sigma^2 S^2\, dt$$. Substituting \eqref{eq.gbm} into \eqref{eq.ito}:

\begin{equation}\label{eq.dV}
dV = \underbrace{\left(\frac{\partial V}{\partial t} + \mu S\frac{\partial V}{\partial S}
     + \frac{1}{2}\sigma^2 S^2 \frac{\partial^2 V}{\partial S^2}\right)}_{\text{drift}} dt
   + \underbrace{\sigma S \frac{\partial V}{\partial S}}_{\text{diffusion}}\, dW_t.
\end{equation}

The second-order term $$\frac{1}{2}\sigma^2 S^2 \partial^2 V/\partial S^2$$, absent in
classical calculus, is the hallmark of Ito's lemma.

### Delta hedging and the Black-Scholes PDE

The key insight is to construct a **self-financing, instantaneously risk-free portfolio**
$$\Pi$$ by holding one long option and shorting $$\Delta = \partial V/\partial S$$ units
of the underlying stock:

\begin{equation}
\Pi = V - \frac{\partial V}{\partial S}\, S.
\end{equation}

The instantaneous change in portfolio value is

\begin{equation}
d\Pi = dV - \frac{\partial V}{\partial S}\, dS
     = \left(\frac{\partial V}{\partial t}
       + \frac{1}{2}\sigma^2 S^2 \frac{\partial^2 V}{\partial S^2}\right) dt,
\end{equation}

where the stochastic term $$dW_t$$ has cancelled exactly — the portfolio is risk-free over
the interval $$dt$$. By the **no-arbitrage principle** it must earn the risk-free rate
$$r$$:

\begin{equation}
d\Pi = r\Pi\, dt = r\!\left(V - S\frac{\partial V}{\partial S}\right) dt.
\end{equation}

Equating the two expressions for $$d\Pi$$ and rearranging yields the
**Black-Scholes PDE**:

\begin{equation}\label{eq.bspde}
\boxed{\frac{\partial V}{\partial t} + \frac{1}{2}\sigma^2 S^2 \frac{\partial^2 V}{\partial S^2}
+ rS\frac{\partial V}{\partial S} - rV = 0.}
\end{equation}

Remarkably, the drift $$\mu$$ has vanished entirely. The fair price of any derivative is
independent of the expected return on the stock — only its volatility $$\sigma$$ and the
risk-free rate $$r$$ enter.

### Boundary and terminal conditions

The PDE \eqref{eq.bspde} must be supplemented with conditions that identify the
particular contract being priced.

For a European **call**:
\begin{equation}
C(S,T) = \max(S-K,0), \quad C(0,t) = 0, \quad C(S,t) \sim S - Ke^{-r(T-t)} \text{ as } S\to\infty.
\end{equation}

For a European **put**:
\begin{equation}
P(S,T) = \max(K-S,0), \quad P(0,t) = Ke^{-r(T-t)}, \quad P(S,t)\to 0 \text{ as } S\to\infty.
\end{equation}

### Solution: reduction to the heat equation

The Black-Scholes PDE is equivalent to the classical **heat equation**, allowing its
explicit solution.

**Step 1: log-price variable.** Set $$x = \ln(S/K)$$, $$\tau = T - t$$, and
$$V(S,t) = K\, v(x,\tau)$$. Substituting into \eqref{eq.bspde} (with the sign of the
time derivative flipped because $$\tau$$ increases backwards in time):

\begin{equation}
\frac{\partial v}{\partial \tau}
= \frac{1}{2}\sigma^2 \frac{\partial^2 v}{\partial x^2}
+ \left(r - \tfrac{1}{2}\sigma^2\right)\frac{\partial v}{\partial x} - rv.
\end{equation}

**Step 2: remove first-order and zeroth-order terms.** Write
$$v(x,\tau) = e^{\alpha x + \beta\tau} u(x,\tau)$$ with

\begin{equation}
\alpha = -\frac{r - \frac{1}{2}\sigma^2}{\sigma^2}, \qquad
\beta  = -\frac{\left(r-\frac{1}{2}\sigma^2\right)^2}{2\sigma^2} - r.
\end{equation}

The equation for $$u$$ becomes the **heat equation**:

\begin{equation}\label{eq.heat}
\frac{\partial u}{\partial \tau} = \frac{\sigma^2}{2}\frac{\partial^2 u}{\partial x^2}.
\end{equation}

**Step 3: solve by convolution.** The solution to \eqref{eq.heat} with initial data
$$u(x,0) = u_0(x)$$ is

\begin{equation}
u(x,\tau) = \frac{1}{\sigma\sqrt{2\pi\tau}}
             \int_{-\infty}^{\infty} u_0(s)\,
             e^{-(x-s)^2/(2\sigma^2\tau)}\, ds.
\end{equation}

**Step 4: transform the call payoff.** The terminal condition $$C(S,T)=\max(S-K,0)$$
translates to

$$
u_0(x) = K\left(e^{(1-\alpha)x} - e^{-\alpha x}\right)\mathbf{1}_{x>0}.
$$

Evaluating the Gaussian integral by completing the square twice recovers the celebrated
closed-form formula.

### The Black-Scholes formula

Define the time to expiry $$\tau = T-t$$ and the quantities

\begin{equation}\label{eq.d1d2}
d_1 = \frac{\ln(S/K) + \left(r + \frac{1}{2}\sigma^2\right)\tau}{\sigma\sqrt{\tau}},
\qquad
d_2 = d_1 - \sigma\sqrt{\tau}
    = \frac{\ln(S/K) + \left(r - \frac{1}{2}\sigma^2\right)\tau}{\sigma\sqrt{\tau}}.
\end{equation}

The price of a European **call** is

\begin{equation}\label{eq.call}
\boxed{C(S,t) = S\,\Phi(d_1) - K e^{-r\tau}\,\Phi(d_2),}
\end{equation}

and the price of a European **put** is

\begin{equation}\label{eq.put}
\boxed{P(S,t) = K e^{-r\tau}\,\Phi(-d_2) - S\,\Phi(-d_1),}
\end{equation}

where $$\Phi(x) = \frac{1}{\sqrt{2\pi}}\int_{-\infty}^x e^{-s^2/2}\,ds$$ is the
standard normal CDF.

**Interpretation.** Under the risk-neutral measure (see below):
- $$\Phi(d_2)$$ is the probability that the call expires in-the-money, i.e.\ $$\mathbb{Q}[S_T > K]$$;
- $$S\,\Phi(d_1)$$ is the expected present value of receiving $$S_T$$ conditional on finishing in-the-money, discounted at rate $$r$$.

Thus the call price is simply the discounted expected value of the payoff $$\max(S_T-K,0)$$.

### Put-call parity

A model-independent no-arbitrage relation connects call and put prices with the same
strike and expiry:

\begin{equation}\label{eq.pcp}
C - P = S - Ke^{-r\tau}.
\end{equation}

To prove it, observe that a portfolio long one call and short one put replicates a forward
contract: its payoff is $$(S_T-K)$$ regardless of the direction of the market. Discounting
that payoff gives the right-hand side. The Black-Scholes formulas \eqref{eq.call} and
\eqref{eq.put} are automatically consistent with \eqref{eq.pcp} via the identity
$$\Phi(x) + \Phi(-x) = 1$$.

### The Greeks

The partial derivatives of the option price quantify its sensitivities and are collectively
called the **Greeks**. Let $$\phi(x) = \Phi'(x) = e^{-x^2/2}/\sqrt{2\pi}$$ denote the
standard normal PDF.

**Delta** $$(\Delta)$$ — sensitivity to the underlying price, and the hedge ratio:
\begin{equation}
\Delta_C = \frac{\partial C}{\partial S} = \Phi(d_1),
\qquad
\Delta_P = \frac{\partial P}{\partial S} = \Phi(d_1) - 1.
\end{equation}
Delta lies in $$[0,1]$$ for calls and $$[-1,0]$$ for puts. An at-the-money option has $$\Delta \approx \pm 0.5$$.

**Gamma** $$(\Gamma)$$ — rate of change of delta; curvature of the price surface:
\begin{equation}
\Gamma = \frac{\partial^2 V}{\partial S^2} = \frac{\phi(d_1)}{S\sigma\sqrt{\tau}}.
\end{equation}
Gamma is identical for calls and puts (by put-call parity). It is largest for
at-the-money options near expiry.

**Theta** $$(\Theta)$$ — time decay; how much value is lost per unit time:
\begin{equation}
\Theta_C = \frac{\partial C}{\partial t}
         = -\frac{S\phi(d_1)\sigma}{2\sqrt{\tau}} - rKe^{-r\tau}\Phi(d_2).
\end{equation}
$$\Theta < 0$$ for long option positions — the option loses value as expiry approaches,
all else equal.

**Vega** $$({\cal V})$$ — sensitivity to volatility:
\begin{equation}
\mathcal{V} = \frac{\partial V}{\partial\sigma} = S\phi(d_1)\sqrt{\tau}.
\end{equation}
Vega is the same for calls and puts and is always positive: higher volatility increases
the probability of a large move, benefiting the option holder.

**Rho** $$(\rho)$$ — sensitivity to the risk-free interest rate:
\begin{equation}
\rho_C = \frac{\partial C}{\partial r} = K\tau\, e^{-r\tau}\Phi(d_2),
\qquad
\rho_P = -K\tau\, e^{-r\tau}\Phi(-d_2).
\end{equation}

The Greeks satisfy a linear identity that is simply a restatement of the Black-Scholes PDE \eqref{eq.bspde}:
\begin{equation}
\Theta + \tfrac{1}{2}\sigma^2 S^2\,\Gamma + rS\,\Delta - rV = 0.
\end{equation}
This means that the time decay $$\Theta$$ of a delta-hedged position is financed exactly
by the gamma profit $$\frac{1}{2}\sigma^2 S^2 \Gamma$$.

### Risk-neutral pricing

A deeper, measure-theoretic derivation of the Black-Scholes formula uses the theory of
**risk-neutral (martingale) measures**. By the fundamental theorem of asset pricing, the
absence of arbitrage is equivalent to the existence of an equivalent probability measure
$$\mathbb{Q}$$ under which every discounted asset price is a martingale.

By **Girsanov's theorem**, under $$\mathbb{Q}$$ the Brownian motion is shifted by the
*market price of risk* $$\lambda = (\mu - r)/\sigma$$:
$$
\widetilde{W}_t = W_t + \lambda t,
$$
and the stock dynamics become

\begin{equation}
dS = r S\, dt + \sigma S\, d\widetilde{W}_t.
\end{equation}

The drift is replaced by $$r$$ — under $$\mathbb{Q}$$, all assets grow at the risk-free
rate. Using \eqref{eq.lognormal} with $$\mu\to r$$, the stock at expiry is

\begin{equation}
S_T = S\exp\!\left[\left(r - \tfrac{1}{2}\sigma^2\right)\tau + \sigma\sqrt{\tau}\,Z\right],
\quad Z\overset{\mathbb{Q}}{\sim}\mathcal{N}(0,1).
\end{equation}

The no-arbitrage price of any derivative with bounded payoff $$f(S_T)$$ is then

\begin{equation}\label{eq.rn}
V(S,t) = e^{-r\tau}\,\mathbb{E}^{\mathbb{Q}}\!\left[f(S_T)\,\big|\,S_t=S\right].
\end{equation}

For a call, $$f(S_T)=\max(S_T-K,0)$$. Splitting the expectation into the region
$$S_T>K$$ and completing the square in the exponent recovers \eqref{eq.call} exactly.
The risk-neutral framework is more general than the PDE approach: it applies to
path-dependent, American, and multi-asset derivatives where no closed-form PDE exists.

### Dividends

When the underlying pays a continuous dividend yield $$q$$, shareholders receive a
cash flow $$qS\,dt$$ per unit time. The stock dynamics become

\begin{equation}
dS = (\mu - q)S\, dt + \sigma S\, dW_t.
\end{equation}

Under the risk-neutral measure the drift becomes $$(r-q)$$, and the Black-Scholes
formula is modified via **Merton's extension** (1973):

\begin{equation}
d_1 = \frac{\ln(S/K) + \left(r - q + \frac{1}{2}\sigma^2\right)\tau}{\sigma\sqrt{\tau}},
\qquad
d_2 = d_1 - \sigma\sqrt{\tau},
\end{equation}

with the call price becoming $$C = S e^{-q\tau}\Phi(d_1) - Ke^{-r\tau}\Phi(d_2)$$.
Currency options follow the same formula with the foreign risk-free rate playing the role
of $$q$$ (the Garman-Kohlhagen model).

### Assumptions and limitations

The Black-Scholes model rests on several idealizing assumptions:

1. **Constant volatility.** In practice, implied volatility varies with strike and
   maturity — the *volatility smile* or *skew* — a systematic deviation from the model.
   Extensions include Dupire's local volatility model (1994), where $$\sigma = \sigma(S,t)$$,
   and stochastic volatility models such as Heston (1993), where $$\sigma$$ itself follows
   a mean-reverting diffusion.

2. **Log-normal returns.** Real returns exhibit heavy tails (excess kurtosis) and
   negative skewness. This leads to systematic mis-pricing of deep out-of-the-money
   options, which is precisely the origin of the volatility smile observed after the 1987
   crash.

3. **Continuous, frictionless trading.** Continuous delta hedging is impossible in
   practice. Discrete rebalancing introduces **hedging error** proportional to the
   gamma of the position.

4. **No transaction costs or liquidity constraints.** Incorporating costs leads to
   non-linear PDEs (Leland 1985) and option price intervals rather than unique prices.

5. **Constant risk-free rate.** Interest rate risk is non-trivial for long-dated options.
   Term-structure models (Vasicek, Hull-White, CIR) address this.

Despite these limitations, Black-Scholes remains the lingua franca of options markets.
Practitioners quote prices in **implied volatility** $$\sigma_{\mathrm{imp}}$$ — the
value of $$\sigma$$ that equates \eqref{eq.call} to the observed market price — because
the formula provides an invertible, universal mapping between prices and volatilities.
In this sense, implied volatility is not a prediction but a convenient re-parameterization
of price that facilitates comparison across strikes, expiries, and underlyings.
