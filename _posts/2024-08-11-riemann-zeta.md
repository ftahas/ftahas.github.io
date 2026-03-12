---
layout: page
title: Riemann hypothesis
date: 2024-08-11 11:12:00-0400
description: Riemann zeta function and its zeros
img: 
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

$$
\zeta(z) = 1+\frac{1}{2}+\frac{1}{3} + \frac{1}{4}+\frac{1}{5}+\dots = \sum_{n=1}^\infty \frac{1}{n}.
$$

To understand how this apparently non-divergent series diverges, consider an integral instead of a sum

$$
\int_1^N \frac{1}{x} dx = \log(N).
$$

As we know that the sum is approximately equal the integral, at least it scales equally and the difference is well-known and it is called Euler-Mascheroni constant $$\gamma$$

$$
\sum_{n=1}^N \frac{1}{n} = \int_1^N \frac{1}{x} dx + \gamma = \log(N) +\gamma.
$$

Therefore, as $$\log(N)$$ has no upper bound, i.e. $$\lim_{N\to \infty} \log(N) \to \infty$$, the sum also diverges as $$N\to \infty$$.

Now, instead let's consider the integral representation of the zeta function provided by
\begin{equation}\label{eq.zeta2}
\zeta(z)= \frac{1}{\Gamma(z)} \int_0^\infty dt \, \frac{t^{z-1}}{e^{t}-1},
\end{equation}
where
\begin{equation}
\Gamma(z) = \int_0^\infty dt \, e^{-t} t^{z-1},
\end{equation}
is the gamma function. In order to realize its range of validity, we observe that the integrand at small $$t$$. The denominator approaches $$t$$, thence the integrand is $$t^{z-2}$$ at small $$t$$:
\begin{equation}
t^{z-2} = t^{\mathrm{Re}(z) -2} t^{i \mathrm{Im}(z)},
\end{equation}
and it will converge for values obeying $$\mathrm{Re}(z) >1$$.

Let us now call the right-hand side of \eqref{eq.zeta2} $$I$$ and multiply the integrand by $$e^{-t}/e^{-t}$$ and perform an expansion in powers of $$e^{-t}$$:

$$
I = \frac{1}{\Gamma(z)} \int_0^\infty dt \, \frac{t^{z-1} e^{-t}}{1-e^{-t}} = \frac{1}{\Gamma(z)} \int_0^\infty dt \, \sum_{n=1}^\infty t^{z-1}e^{-nt} .
$$

Now, changing the integration variable $$t\to t/n$$ we have that:

$$
I = \frac{1}{\Gamma(z)} \int_0^\infty \, \sum_{n=1}^\infty \left(\frac{t}{n}\right)^{z-1} e^{-t} \frac{dt}{n} = \frac{1}{\Gamma(z)} \sum_{n=1}^\infty \frac{1}{n^z} \int_0^\infty dt \, t^{z-1} e^{-t} = \frac{\zeta(z)}{\Gamma(z)} \int_0^\infty dt \, t^{z-1} e^{-t} = \zeta(z).
$$


The integral representation \eqref{eq.zeta2} thus provides an equivalent definition of $$\zeta(z)$$ for $$\mathrm{Re}(z)>1$$.

### Functional equation and analytic continuation

To extend $$\zeta(z)$$ to the rest of the complex plane, one uses the **functional equation** discovered by Riemann:
\begin{equation}\label{eq.functional}
\zeta(z) = 2^z \pi^{z-1} \sin\!\left(\frac{\pi z}{2}\right) \Gamma(1-z)\, \zeta(1-z).
\end{equation}

This remarkable identity relates the value of $$\zeta$$ at $$z$$ to its value at $$1-z$$, effectively reflecting the function about the line $$\mathrm{Re}(z) = \tfrac{1}{2}$$. Since the right-hand side is well-defined (away from the poles of $$\Gamma$$ and the zero of $$\sin$$) for $$\mathrm{Re}(z)<0$$, and the series definition covers $$\mathrm{Re}(z)>1$$, the functional equation provides the analytic continuation to the entire complex plane except for the simple pole at $$z=1$$.

A symmetric form of \eqref{eq.functional} is obtained by introducing the **completed zeta function**
\begin{equation}
\xi(z) = \frac{1}{2}z(z-1)\pi^{-z/2}\Gamma\!\left(\frac{z}{2}\right)\zeta(z),
\end{equation}
which satisfies the clean relation $$\xi(z) = \xi(1-z)$$.

### Zeros of the zeta function

The zeros of $$\zeta(z)$$ fall into two classes.

**Trivial zeros.** The factor $$\sin(\pi z/2)$$ in \eqref{eq.functional} vanishes at $$z = -2, -4, -6, \dots$$. These are cancelled by the poles of $$\Gamma(1-z)$$ only partially, so $$\zeta(z)=0$$ at every negative even integer:
$$
\zeta(-2) = \zeta(-4) = \zeta(-6) = \dots = 0.
$$

**Non-trivial zeros.** All remaining zeros lie in the **critical strip** $$0 < \mathrm{Re}(z) < 1$$. The functional equation implies that if $$\rho$$ is a non-trivial zero, so is $$1-\rho$$. Because $$\zeta$$ has real coefficients, $$\bar{\rho}$$ and $$1-\bar{\rho}$$ are zeros as well, so non-trivial zeros come in quadruples symmetric about both the real axis and the critical line $$\mathrm{Re}(z)=\tfrac{1}{2}$$.

Numerical computation reveals the first few non-trivial zeros at
$$
\rho_1 \approx \tfrac{1}{2} + 14.135\, i, \quad \rho_2 \approx \tfrac{1}{2} + 21.022\, i, \quad \rho_3 \approx \tfrac{1}{2} + 25.011\, i, \quad \dots
$$
all of which lie exactly on the critical line $$\mathrm{Re}(z) = \tfrac{1}{2}$$.

### The Riemann Hypothesis

In his 1859 paper Riemann conjectured that **every non-trivial zero of $$\zeta(z)$$ has real part equal to $$\tfrac{1}{2}$$**, i.e.\ all non-trivial zeros lie on the critical line.

This is the **Riemann Hypothesis**, one of the Millennium Prize Problems and widely considered the most important unsolved problem in mathematics. Its truth has been verified computationally for the first $$10^{13}$$ zeros, yet a general proof remains elusive.

The hypothesis has deep consequences for the distribution of prime numbers. The **prime-counting function** $$\pi(x)$$ — the number of primes less than or equal to $$x$$ — is approximated by the logarithmic integral $$\mathrm{Li}(x)$$, and the error in this approximation is controlled by the zeros of $$\zeta$$:
\begin{equation}
\pi(x) = \mathrm{Li}(x) - \sum_{\rho} \mathrm{Li}(x^\rho) + \cdots
\end{equation}
If the Riemann Hypothesis holds, the error satisfies $$|\pi(x) - \mathrm{Li}(x)| = O(\sqrt{x}\log x)$$, the best possible bound.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/zeta.jpg" title="Riemann zeta" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>


[Notes here](../assets/pdf/Riemann_zeta.pdf)