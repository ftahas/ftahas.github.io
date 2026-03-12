---
layout: page
title: Quantum Entanglement
date: 2025-07-12 11:00:00-0400
description: Bell states, the EPR paradox, Bell inequalities, and the experimental violation of local realism
tags: physics quantum-mechanics
categories: fun
related_posts: false
---

**Quantum entanglement** is arguably the most striking departure from classical physics: two particles can share a quantum state such that measurements on them are correlated in ways that no classical local theory can explain. Einstein called it *spukhafte Fernwirkung* — "spooky action at a distance" — and spent decades trying to explain it away. Bell's theorem and subsequent experiments show he was wrong.

### Composite systems and the tensor product

In quantum mechanics, the Hilbert space of a composite system is the **tensor product** of the subsystem spaces:

\begin{equation}
\mathcal{H}_{AB} = \mathcal{H}_A \otimes \mathcal{H}_B.
\end{equation}

A state $$|\psi\rangle_{AB} \in \mathcal{H}_{AB}$$ is **separable** if it can be written as $$|\psi\rangle = |\phi\rangle_A \otimes |\chi\rangle_B$$. Otherwise, it is **entangled** — it cannot be factored into a product of states for each subsystem.

### Bell states

The four **maximally entangled** two-qubit states (Bell basis):

\begin{equation}
|\Phi^\pm\rangle = \frac{1}{\sqrt{2}}\left(|00\rangle \pm |11\rangle\right), \qquad
|\Psi^\pm\rangle = \frac{1}{\sqrt{2}}\left(|01\rangle \pm |10\rangle\right).
\end{equation}

Consider $$|\Psi^-\rangle = \frac{1}{\sqrt{2}}(|01\rangle - |10\rangle)$$: if Alice measures spin-up along any axis, Bob's particle is immediately in the spin-down state along that same axis — regardless of the spatial separation between them.

### The EPR paradox

Einstein, Podolsky, and Rosen (1935) argued that quantum mechanics is **incomplete**. Their argument: for $$|\Psi^-\rangle$$, Alice can measure along $$\hat{x}$$ or $$\hat{z}$$ and predict Bob's outcome with certainty. Since Alice's measurement cannot physically disturb Bob's distant particle, Bob's particle must have had a definite value along both axes *before* measurement. But quantum mechanics forbids simultaneous definite values for non-commuting observables ($$[\hat{\sigma}_x, \hat{\sigma}_z] \neq 0$$). Therefore, quantum mechanics must be incomplete — there must be **hidden variables** completing the description.

### Bell's theorem

John Bell (1964) showed that **any** local hidden variable (LHV) theory — one in which measurement outcomes are determined by pre-existing hidden variables, and in which no signal travels faster than light — satisfies an inequality that **quantum mechanics violates**.

Consider spin measurements along directions $$\hat{a}, \hat{b}, \hat{c}$$ on the singlet $$|\Psi^-\rangle$$. The **CHSH inequality** (Clauser, Horne, Shimony, Holt, 1969) states that for any LHV theory:

\begin{equation}\label{eq.CHSH}
|S| \leq 2, \quad S = E(a, b) - E(a, b') + E(a', b) + E(a', b'),
\end{equation}

where $$E(\hat{n}, \hat{m}) = \langle \hat{\sigma}_A\cdot\hat{n}\;\hat{\sigma}_B\cdot\hat{m}\rangle$$ is the correlation between the two outcomes.

**Quantum prediction**: for the singlet, $$E(\hat{n}, \hat{m}) = -\cos\theta_{nm}$$. Choosing $$\hat{a}$$ at $$0°$$, $$\hat{a}'$$ at $$90°$$, $$\hat{b}$$ at $$45°$$, $$\hat{b}'$$ at $$-45°$$:

\begin{equation}
S_{\rm QM} = -\cos45° - \cos(-45°) - \cos45° - \cos135° = 2\sqrt{2} \approx 2.828.
\end{equation}

Quantum mechanics violates \eqref{eq.CHSH} by a factor $$\sqrt{2}$$. This is the **Tsirelson bound** — the maximum quantum violation.

### Experimental tests

A succession of increasingly rigorous experiments confirmed the quantum prediction:

| Experiment | Year | $$\lvert S\rvert$$ measured | Loopholes closed |
|---|---|---|---|
| Freedman–Clauser | 1972 | $$2.00 \pm 0.05$$ | First test |
| Aspect et al. | 1982 | $$2.697 \pm 0.015$$ | Locality |
| Weihs et al. | 1998 | $$2.731 \pm 0.026$$ | Fast switching |
| Hensen et al. | 2015 | $$2.42 \pm 0.20$$ | **Both** (loophole-free) |
| Giustina et al. | 2015 | $$2.37 \pm 0.09$$ | Both |

The 2015 loophole-free experiments closed simultaneously the **locality loophole** (settings chosen after particles are separated) and the **detection loophole** (high-efficiency detectors). Local hidden variable theories are experimentally ruled out. The 2022 Nobel Prize in Physics was awarded to Aspect, Clauser, and Zeilinger for this work.

### Entanglement entropy

For a pure state $$|\psi\rangle_{AB}$$, the degree of entanglement is measured by the **von Neumann entropy** of the reduced density matrix:

\begin{equation}
S_A = -\mathrm{Tr}(\rho_A \ln \rho_A), \quad \rho_A = \mathrm{Tr}_B(|\psi\rangle\langle\psi|).
\end{equation}

For a Bell state, $$\rho_A = \frac{1}{2}\mathbb{1}$$ and $$S_A = \ln 2$$ (one ebit of entanglement). For a product state, $$S_A = 0$$.

The **Schmidt decomposition** guarantees that any bipartite pure state can be written as $$|\psi\rangle = \sum_k \lambda_k |\alpha_k\rangle_A|\beta_k\rangle_B$$ with $$\lambda_k \geq 0$$, $$\sum_k\lambda_k^2 = 1$$. Entanglement iff more than one Schmidt coefficient is non-zero.

### Applications

**Quantum teleportation** (Bennett et al., 1993): transmit an arbitrary qubit state $$|\phi\rangle$$ using one Bell pair and two classical bits, without physically transmitting the qubit. The state is reconstructed at the receiver via local unitaries conditioned on the classical message.

**Superdense coding**: transmit two classical bits by sending one qubit, using pre-shared entanglement — doubling the classical capacity of a quantum channel.

**Quantum key distribution** (E91 protocol, Ekert 1991): the Bell inequality violation itself certifies that an eavesdropper has not tampered with the shared key — device-independent security.

**Entanglement as a resource** underlies all of quantum computing's potential speedups: Shor's factoring algorithm, Grover's search, quantum simulation of many-body systems. The study of **entanglement structure** — area laws, topological entanglement entropy, tensor network states — is now a cornerstone of condensed matter and quantum gravity.
