---
layout: post
title: Riemann hypothesis
date: 2024-08-11 11:12:00-0400
description: Riemann zeta function and its zeros
tags: math
categories: fun
related_posts: false
---

### Riemann zeta function

The Riemann zeta function is defined as

\begin{equation}\label{eq.zeta1}
\zeta(z) = 1+\frac{1}{2^z}+\frac{1}{3^z} + \frac{1}{4^z}+\frac{1}{5^z}+\dots = \sum\_{n=1}^\infty \frac{1}{n^{z}}.
\end{equation}

The Riemann zeta function is connected to prime numbers through the Euler product representation:
\begin{equation}
\zeta(z) = \prod\_{p \in \mathbb{P}} \frac{1}{1-p^{-z}}, \quad \mathbb{P} = \{2,3,5,7,11,13,17,19,\dots \},
\end{equation}
$$\mathbb{P}$$ is the set of prime numbers.

The proof of the Euler product expansion is quite simple and elegant.
Firstly, let's multiply the Riemann zeta function by $$\frac{1}{2^z}$$
\begin{equation}
\frac{1}{2^z} \zeta(z) = \frac{1}{2^z}+ \frac{1}{4^z}+\frac{1}{6^z} + \frac{1}{8^z} \dots
\end{equation}
Subtract it from the Rzf
\begin{equation}
\left(1- \frac{1}{2^z} \right) \zeta(z) = 1+\frac{1}{3^z} +\frac{1}{5^z}+ \frac{1}{7^z} + \frac{1}{9^z} + \frac{1}{11^z} + \dots.
\end{equation}
we see that all multiples of 2 are gone.
Multiplying the result by $$\frac{1}{3^z}$$:
\begin{equation}
\frac{1}{3^z}\left(1- \frac{1}{2^z} \right) \zeta(z) = \frac{1}{3^z} +\frac{1}{9^z}+ \frac{1}{15^z}+ \frac{1}{21^z} + \frac{1}{27^z} + \frac{1}{33^z} + \dots,
\end{equation}
and subtracting again we have
\begin{equation}
\left(1- \frac{1}{3^z} \right)\left(1- \frac{1}{2^z} \right) \zeta(z) = 1+ \frac{1}{5^z}+ \frac{1}{7^z}+ \frac{1}{11^z} + \frac{1}{13^z} + \frac{1}{17^z} + \dots,
\end{equation}
and now all the terms multiple of 3 are gone.
If we keep multiply by $$1/p^z$$ where $$p$$ is a prime number, we will eventually get rid of all terms and be only left with 1, as all numbers can be factorized as a product of prime numbers. Thence,
\begin{equation}
\dots \times \left(1- \frac{1}{11^z} \right)\left(1- \frac{1}{7^z} \right)\left(1- \frac{1}{5^z} \right)\left(1- \frac{1}{3^z} \right)\left(1- \frac{1}{2^z} \right) \zeta(z) = 1,
\end{equation}
proving that
\begin{equation}
\zeta(z) = \prod\_{p \in \mathbb{P}} \frac{1}{1-p^{-z}}.
\end{equation}

### Range of validity and analytic continuation

We see from \eqref{eq.zeta1} converges whenever $$\mathbb{Re} z>1$$. It has a known pole at $$z=1$$:  
\begin{equation}
\zeta(z) = 1+\frac{1}{2}+\frac{1}{3} + \frac{1}{4}+\frac{1}{5}+\dots = \sum*{n=1}^\infty \frac{1}{n}.
\end{equation}
To understand how this apparently non-divergent series diverges, consider an integral instead of a sum
\begin{equation}
\int_1^N \frac{1}{x} dx = \log(N).
\end{equation}
As we know that the sum is approximately equal the integral, at least it scales equally and the difference is well-known and it is called Euler-Mascheroni constant $$\gamma$$
\begin{equation}
\sum*{n=1}^N \frac{1}{n} = \int*1^N \frac{1}{x} dx + \gamma = \log(N) +\gamma.
\end{equation}
Therefore, as $$\log(N)$$ has no upper bound, i.e. $$\lim\_{N\to \infty} \log(N) \to \infty$$, the sum also diverges as $$N\to \infty$$.

Now, instead let's consider the integral representation of the zeta function provided by
\begin{equation}\label{eq.zeta2}
\zeta(z)= \frac{1}{\Gamma(z)} \int_0^\infty dt \, \frac{t^{z-1}}{e^{t}-1},
\end{equation}
where
\begin{equation}
\Gamma(z) = \int_0^\infty dt \, e^{-t} t^{z-1} ,
\end{equation}
is the gamma function. In order to realize its range of validity, we observe that the integrand at small $$t$$. The denominator approaches $$t$$, thence the integrand is $$t^{z-2}$$ at small $$t$$:
\begin{equation}
t^{z-2} = t^{\mathrm{Re}(z) -2} t^{i \mathrm{Im}(z)},
\end{equation}
and it will converge for values obeying $$\mathrm{Re}(z) >1$$.

Let us now call the right-hand side of \eqref{eq.zeta2} $$I$$ and multiply the integrand by $$e^{-t}/e^{-t}$$ and perform an expansion in powers of $$e^{-t}$$:
$$
I = \frac{1}{\Gamma(z)} \int\_0^\infty dt \, \frac{t^{z-1} e^{-t}}{1-e^{-t}} = \frac{1}{\Gamma(z)} \int_0^\infty dt \, \sum*{n=1}^\infty t^{z-1}e^{-nt} .
$$
Now, changing the integration variable $$t\to t/n$$:
$$
I = \frac{1}{\Gamma(z)} \int*0^\infty \, \sum*{n=1}^\infty \left(\frac{t}{n}\right)^{z-1} e^{-t} \frac{dt}{n} = \frac{1}{\Gamma(z)} \sum\_{n=1}^\infty \frac{1}{n^z} \int_0^\infty dt \, t^{z-1} e^{-t} = \frac{\zeta(z)}{\Gamma(z)} \int_0^\infty dt \, t^{z-1} e^{-t} = \zeta(z).
$$

To be continued ...
