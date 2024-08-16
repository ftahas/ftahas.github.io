---
layout: post
title: Riemann hypothesis
date: 2024-08-11 11:12:00-0400
description: Riemann zeta function and its zeros 
tags: math
categories: fun
related_posts: false
---

For $$ \mathrm{Re}(z)>1 $$, the Riemann zeta function is defined as 

\begin{equation}
\zeta(z) = 1+\frac{1}{2^z}+\frac{1}{3^z} + \frac{1}{4^z}+\frac{1}{5^z}+\dots = \sum_{n=1}^\infty \frac{1}{n^{z}}= \frac{1}{\Gamma(z)} \int_0^\infty dx \, \frac{x^{z-1}}{e^{z}-1},
\end{equation}


The Riemann zeta function is connected to prime numbers through the Euler product representation: 
\begin{equation}
\zeta(z) = \prod_{p \in \mathbb{P}} \frac{1}{1-p^{-z}}, \quad \mathbb{P} = \{2,3,5,7,11,13,17,19,\dots \}
\end{equation}
$$ \mathbb{P} $$ is the set of prime numbers. 



The proof of the Euler product expansion is quite simple and elegant. 
Firstly, let's multiply the Riemann zeta function by $$\frac{1}{2^z}$$
\begin{equation}
  \frac{1}{2^z}  \zeta(z) =  \frac{1}{2^z}+ \frac{1}{4^z}+\frac{1}{6^z} + \frac{1}{8^z} \dots
\end{equation}
Subtract it from the Rzf 
\begin{equation}
\left(1-  \frac{1}{2^z} \right) \zeta(z) =  1+\frac{1}{3^z} +\frac{1}{5^z}+  \frac{1}{7^z} + \frac{1}{9^z} + \frac{1}{11^z} +  \dots.
\end{equation}
we see that all multiples of $$2$$ are gone. 
Multiplying the result by $$\frac{1}{3^z}$$: 
\begin{equation}
\frac{1}{3^z}\left(1-  \frac{1}{2^z} \right) \zeta(z) =  \frac{1}{3^z} +\frac{1}{9^z}+ \frac{1}{15^z}+  \frac{1}{21^z} + \frac{1}{27^z} + \frac{1}{33^z} +  \dots,
\end{equation}
and subtracting again we have 
\begin{equation}
\left(1-  \frac{1}{3^z} \right)\left(1-  \frac{1}{2^z} \right) \zeta(z) = 1+ \frac{1}{5^z}+ \frac{1}{7^z}+  \frac{1}{11^z} + \frac{1}{13^z} + \frac{1}{17^z} +  \dots,
\end{equation}
and now all the terms multiple of $$3$$ are gone. 
If we keep multiply by $$1/p^z$$ where $$p$$ is a prime number, we will eventually get rid of all terms and be only left with $$1$$, as all numbers can be factorized as a product of prime numbers. Thence, 
\begin{equation}
\dots \times \left(1-  \frac{1}{11^z} \right)\left(1-  \frac{1}{7^z} \right)\left(1-  \frac{1}{5^z} \right)\left(1-  \frac{1}{3^z} \right)\left(1-  \frac{1}{2^z} \right) \zeta(z) = 1,
\end{equation}
proving that 
\begin{equation}
    \zeta(z) = \prod_{p \in \mathbb{P}} \frac{1}{1-p^{-z}}.
\end{equation}



To be continued ...