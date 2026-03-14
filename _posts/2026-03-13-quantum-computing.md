---
layout: page
title: Quantum computing simulations with Qiskit
date: 2026-03-13 12:00:00-0300
description: A tour through quantum gates, entanglement, key algorithms, VQE, and error correction — all simulated on a classical computer
img:
tags: physics math quantum computing
categories: fun
related_posts: false
---

Quantum computing sits at the intersection of quantum mechanics, linear algebra, and information theory.
Unlike classical bits, which are either 0 or 1, quantum bits (qubits) can exist in superpositions
of both states simultaneously, and multiple qubits can become entangled — correlations that have no
classical analogue. The notebooks in my [Quantum-Computing](https://github.com/ftahas/Quantum-Computing)
repository simulate all of this on a classical machine using [Qiskit](https://qiskit.org/) and its
Aer statevector/shot-based simulator.

---

### Qubits and the Bloch sphere

A single qubit is a unit vector in a two-dimensional complex Hilbert space $$\mathcal{H} \cong \mathbb{C}^2$$.
In the computational basis $$\{|0\rangle, |1\rangle\}$$ it reads

\begin{equation}\label{eq.qubit}
|\psi\rangle = \alpha|0\rangle + \beta|1\rangle, \qquad |\alpha|^2 + |\beta|^2 = 1.
\end{equation}

Up to a global phase, any such state can be parameterised by two real angles:

\begin{equation}\label{eq.bloch}
|\psi\rangle = \cos\!\tfrac{\theta}{2}\,|0\rangle + e^{i\phi}\sin\!\tfrac{\theta}{2}\,|1\rangle,
\quad \theta \in [0,\pi],\; \phi \in [0, 2\pi).
\end{equation}

This is the **Bloch sphere** representation: every pure single-qubit state is a point on the unit
sphere, with $$|0\rangle$$ at the north pole and $$|1\rangle$$ at the south pole.

<div class="row justify-content-sm-center">
    <div class="col-sm-11 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/quantum_computing/qc_sim_cell4_img0.png" title="Single-qubit states on the Bloch sphere under X, H, and Z·H gates" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Four Bloch sphere representations: the initial state \(|0\rangle\), after an X gate \((|1\rangle)\),
    after a Hadamard gate \((|{+}\rangle)\), and after Z·H \((|{-}\rangle)\).
</div>

Single-qubit **gates** are $$2\times 2$$ unitary matrices. The most important ones are:

| Gate | Matrix | Effect on the Bloch sphere |
|------|--------|---------------------------|
| $$X$$ (NOT) | $$\begin{pmatrix}0&1\\1&0\end{pmatrix}$$ | $$\pi$$ rotation about $$x$$ |
| $$Z$$ | $$\begin{pmatrix}1&0\\0&-1\end{pmatrix}$$ | $$\pi$$ rotation about $$z$$ |
| $$H$$ (Hadamard) | $$\tfrac{1}{\sqrt{2}}\begin{pmatrix}1&1\\1&-1\end{pmatrix}$$ | $$\pi$$ rotation about $$(x+z)/\sqrt{2}$$ |
| $$S$$ (phase) | $$\begin{pmatrix}1&0\\0&i\end{pmatrix}$$ | $$\pi/2$$ rotation about $$z$$ |
| $$T$$ | $$\begin{pmatrix}1&0\\0&e^{i\pi/4}\end{pmatrix}$$ | $$\pi/4$$ rotation about $$z$$ |

The Hadamard gate is of particular importance: it maps $$|0\rangle \mapsto |{+}\rangle = (|0\rangle+|1\rangle)/\sqrt{2}$$,
creating a **balanced superposition**. When the resulting state is measured, it yields 0 or 1 with
equal probability — confirmed in simulation with 4096 shots below.

<div class="row justify-content-sm-center">
    <div class="col-sm-7 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/quantum_computing/qc_sim_cell5_img1.png" title="Hadamard gate measurement histogram" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Measurement histogram for \(H|0\rangle\) over 4096 shots. The nearly equal counts for 0 and 1
    confirm the uniform superposition.
</div>

---

### Entanglement and Bell states

A two-qubit system lives in $$\mathbb{C}^2 \otimes \mathbb{C}^2$$ with computational basis
$$\{|00\rangle, |01\rangle, |10\rangle, |11\rangle\}$$. A state is **entangled** if it cannot
be written as a tensor product $$|\psi_A\rangle \otimes |\psi_B\rangle$$.

The four **Bell states** are the canonical maximally-entangled two-qubit states:

\begin{equation}\label{eq.bell}
|\Phi^\pm\rangle = \frac{|00\rangle \pm |11\rangle}{\sqrt{2}}, \qquad
|\Psi^\pm\rangle = \frac{|01\rangle \pm |10\rangle}{\sqrt{2}}.
\end{equation}

Each is prepared by applying a Hadamard gate to the first qubit followed by a CNOT:

$$
|00\rangle \xrightarrow{H\otimes I} \frac{|0\rangle+|1\rangle}{\sqrt{2}}\otimes|0\rangle
\xrightarrow{\mathrm{CNOT}} \frac{|00\rangle+|11\rangle}{\sqrt{2}} = |\Phi^+\rangle.
$$

<div class="row justify-content-sm-center">
    <div class="col-sm-12 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/quantum_computing/qc_sim_cell7_img2.png" title="The four Bell states measurement histograms" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Measurement histograms for the four Bell states \(|\Phi^+\rangle, |\Phi^-\rangle, |\Psi^+\rangle, |\Psi^-\rangle\).
    Each shows perfectly correlated outcomes: only the two basis states composing each Bell state appear,
    each with 50% probability.
</div>

The correlations in \eqref{eq.bell} are what Einstein famously called "spooky action at a distance":
measuring qubit A instantly determines the outcome of measuring qubit B, regardless of separation.
Bell's theorem and subsequent experiments show these correlations cannot be explained by any local
hidden-variable theory.

---

### Quantum algorithms

#### Deutsch–Jozsa

The first algorithm to demonstrate an **exponential** advantage over classical computation was
proposed by Deutsch (1985) and generalised by Jozsa (1992). Given a black-box function
$$f:\{0,1\}^n \to \{0,1\}$$ promised to be either constant (same value on all inputs) or balanced
(exactly half inputs map to 0, half to 1), determine which it is.

- **Classical** deterministic: $$2^{n-1}+1$$ queries in the worst case.
- **Quantum**: exactly **1** query.

The circuit places $$n$$ query qubits in a uniform superposition via $$H^{\otimes n}$$,
applies the oracle $$U_f|x\rangle|y\rangle = |x\rangle|y\oplus f(x)\rangle$$ with the
ancilla qubit in the state $$|{-}\rangle$$, then applies $$H^{\otimes n}$$ again and
measures. A constant oracle leaves all query qubits in $$|0\rangle$$; a balanced oracle
puts them in any state orthogonal to $$|0\cdots0\rangle$$, always yielding a non-zero
measurement result.

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/quantum_computing/qc_sim_cell13_img3.png" title="Deutsch-Jozsa algorithm results for n=3" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Deutsch–Jozsa results for \(n=3\). A constant oracle always outputs \(|000\rangle\)
    (left); a balanced oracle always outputs a non-zero string — here \(|111\rangle\) (right).
    A single oracle call suffices to distinguish the two cases with certainty.
</div>

#### Grover's search

Grover's algorithm (1996) searches an unstructured database of $$N = 2^n$$ items for a
marked element using only $$O(\sqrt{N})$$ oracle queries, compared to $$O(N)$$ classically.
This is a **quadratic** speedup.

Starting from the uniform superposition $$|s\rangle = H^{\otimes n}|0\rangle$$, one
Grover iteration consists of two reflections:

1. **Oracle**: $$O|x\rangle = (-1)^{f(x)}|x\rangle$$ — flips the phase of the target state $$|\omega\rangle$$.
2. **Diffusion**: $$D = 2|s\rangle\langle s| - I$$ — reflects about the mean amplitude.

Each iteration rotates the state vector by $$2\theta$$ in the two-dimensional subspace
spanned by $$|\omega\rangle$$ and its orthogonal complement, where $$\sin\theta = 1/\sqrt{N}$$.
After $$k \approx \tfrac{\pi}{4}\sqrt{N}$$ iterations the overlap with $$|\omega\rangle$$ is maximised.

\begin{equation}
P(|\omega\rangle) \approx \sin^2\!\left((2k+1)\theta\right)
\end{equation}

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/quantum_computing/qc_sim_cell17_img4.png" title="Grover amplitude amplification" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Probability of measuring the target state \(|101\rangle\) as a function of the number of Grover
    iterations for \(n=3\) (\(N=8\)). The probability oscillates sinusoidally, reaching its maximum
    near the theoretically optimal 2 iterations (red dashed line), then overshoots and falls.
</div>

---

### Quantum Fourier Transform

The **Quantum Fourier Transform** (QFT) is the quantum analogue of the discrete Fourier transform.
On an $$n$$-qubit register it implements

\begin{equation}\label{eq.qft}
\mathrm{QFT}|j\rangle = \frac{1}{\sqrt{N}}\sum_{k=0}^{N-1} e^{2\pi i jk/N}|k\rangle, \qquad N=2^n,
\end{equation}

mapping each computational basis state to a superposition with linearly spaced phases.
The DFT on $$N$$ points requires $$O(N\log N)$$ classical operations; the QFT needs only
$$O(n^2)$$ gates — an exponential reduction.

The circuit decomposes into Hadamard gates and controlled phase rotations
$$R_k = \mathrm{diag}(1, e^{2\pi i/2^k})$$, plus a bit-reversal via SWAP gates.

<div class="row justify-content-sm-center">
    <div class="col-sm-12 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/quantum_computing/qft_shor_cell9_img0.png" title="QFT action on computational basis states" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    QFT action for \(n=3\) (\(N=8\)). Top row: input states \(|0\rangle, |1\rangle, |3\rangle, |5\rangle\)
    — each is a single-amplitude spike. Bottom row: corresponding QFT outputs — uniform amplitudes
    with phase structure encoded in color (HSV colormap, radians). The input index determines how fast
    the phase winds around the register.
</div>

#### Quantum Phase Estimation

**Quantum Phase Estimation** (QPE) is the key subroutine in Shor's algorithm and quantum
chemistry solvers. Given a unitary $$U$$ and an eigenstate $$|u\rangle$$ with
$$U|u\rangle = e^{2\pi i\varphi}|u\rangle$$, QPE estimates $$\varphi$$ to $$n$$ bits
of precision using $$n$$ counting qubits and one application of the QFT.

The estimation error is bounded by $$|\hat{\varphi} - \varphi| \leq 2^{-n}$$.

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/quantum_computing/qft_shor_cell15_img2.png" title="QPE precision as a function of counting qubits" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    QPE precision analysis for a true phase \(\varphi = 1/3\). Left: phase estimation error vs.\
    number of counting qubits \(n\) — follows the \(2^{-n}\) bound (dashed). Right: probability of
    the best estimate staying near ~0.67 regardless of \(n\), since \(1/3\) is not exactly
    representable in binary — a finite-precision effect.
</div>

#### Shor's factoring algorithm

Shor's algorithm (1994) reduces integer factorisation to **order finding**: given $$a$$ coprime
to $$N$$, find the smallest $$r$$ such that $$a^r \equiv 1 \pmod{N}$$. QPE applied to the
unitary $$U|y\rangle = |ay \bmod N\rangle$$ yields the order $$r$$ with high probability.
Once $$r$$ is known, the factors of $$N$$ follow from $$\gcd(a^{r/2} \pm 1, N)$$.

The gate count for the modular exponentiation circuit grows **exponentially** with the
number of counting qubits — a major hurdle for near-term hardware:

<div class="row justify-content-sm-center">
    <div class="col-sm-11 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/quantum_computing/qft_shor_cell25_img3.png" title="Shor's circuit resource scaling for N=15, a=7" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Circuit resource scaling for Shor's algorithm (\(N=15\), \(a=7\)). All three metrics —
    circuit depth, equivalent CX gates, and total gate count — grow as \(e^{\sim 0.7n}\) with
    the number of counting qubits. Factoring cryptographically relevant integers (2048-bit RSA)
    would require millions of error-corrected logical qubits.
</div>

---

### Variational Quantum Eigensolver

The **Variational Quantum Eigensolver** (VQE) is a hybrid classical-quantum algorithm designed
for near-term noisy devices. It exploits the **variational principle**:

\begin{equation}\label{eq.vp}
E_0 \leq \langle\psi(\boldsymbol\theta)|\hat{H}|\psi(\boldsymbol\theta)\rangle \equiv E(\boldsymbol\theta),
\end{equation}

where $$|\psi(\boldsymbol\theta)\rangle$$ is a parameterised **ansatz** state prepared by a
quantum circuit, and $$E_0$$ is the true ground-state energy. A classical optimiser minimises
$$E(\boldsymbol\theta)$$ by updating the circuit parameters in a closed loop.

The target here is the H$$_2$$ molecular Hamiltonian (mapped to qubits via Jordan-Wigner):

\begin{equation}
\hat{H} = c_0 I + c_1 Z_0 + c_2 Z_1 + c_3 Z_0 Z_1 + c_4 X_0 X_1 + c_5 Y_0 Y_1,
\end{equation}

with exact ground state energy $$E_0 = -1.771168\;\mathrm{Ha}$$ at equilibrium bond length
$$d = 0.735\;\text{Å}$$.

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/quantum_computing/vqe_cell11_img1.png" title="VQE convergence for H2" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    VQE convergence for H\(_2\) using the RealAmplitudes ansatz (reps=2) and COBYLA optimiser,
    repeated over 5 independent random initialisations. All runs converge to the exact ground state
    energy \(-1.771168\;\mathrm{Ha}\) (red dashed line) within ~40 iterations.
</div>

In practice, quantum computers estimate expectation values through finite **shot noise**:
each Pauli term is measured a finite number of times, introducing statistical error that
scales as $$1/\sqrt{M_\mathrm{shots}}$$. With too few shots the optimiser cannot resolve
the energy landscape:

<div class="row justify-content-sm-center">
    <div class="col-sm-11 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/quantum_computing/vqe_cell19_img5.png" title="VQE convergence under shot noise" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    VQE convergence under shot noise. With only 512 shots/term (left) the optimiser stalls around
    \(-1.62\;\mathrm{Ha}\). At 2048 shots/term (centre) and 8192 shots/term (right) it converges
    progressively closer to the exact value. The trade-off between shot budget and accuracy is
    central to near-term quantum chemistry.
</div>

---

### Quantum error correction

Physical qubits decohere: they suffer **bit-flip** errors ($$X$$), **phase-flip** errors ($$Z$$),
and combinations ($$Y = iXZ$$). Unlike classical bits, quantum states cannot simply be copied
(no-cloning theorem), making error correction non-trivial.

The **3-qubit bit-flip code** encodes one logical qubit $$|\bar{0}\rangle = |000\rangle$$,
$$|\bar{1}\rangle = |111\rangle$$ across three physical qubits. A single-qubit bit-flip
can be detected and corrected via parity measurements without collapsing the logical state.
The logical error rate is

\begin{equation}\label{eq.3bit}
p_L = 3p^2 - 2p^3,
\end{equation}

where $$p$$ is the physical error rate per qubit. For $$p < 1/2$$ we have $$p_L < p$$: the
code improves reliability.

<div class="row justify-content-sm-center">
    <div class="col-sm-11 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/quantum_computing/qec_cell10_img0.png" title="3-qubit bit-flip code performance" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Performance of the 3-qubit bit-flip code. Left: logical error rate \(p_L\) vs.\ physical error
    rate \(p\). The red curve (theory, Eq.\ \eqref{eq.3bit}) matches simulation (blue dots) perfectly;
    for \(p < 1/2\) the code reduces the error. Right: log-scale plot showing the quadratic suppression
    — the hallmark of a distance-3 code.
</div>

More powerful codes — the Shor [[9,1,3]] code, the Steane [[7,1,3]] code, and eventually
the **surface code** — protect against arbitrary single-qubit errors and are the leading
candidates for fault-tolerant quantum computing. The central open problem in the field is
demonstrating that logical error rates can be pushed below the **fault-tolerance threshold**
as the code distance grows — an achievement that would pave the way for running Shor's
algorithm on cryptographically relevant problem sizes.

---

All simulations are available in the [Quantum-Computing](https://github.com/ftahas/Quantum-Computing)
repository, covering these topics and more across four Jupyter notebooks:
[`quantum_computing_simulations.ipynb`](https://github.com/ftahas/Quantum-Computing/blob/main/quantum_computing_simulations.ipynb),
[`qft_shors_algorithm.ipynb`](https://github.com/ftahas/Quantum-Computing/blob/main/qft_shors_algorithm.ipynb),
[`variational_quantum_eigensolver.ipynb`](https://github.com/ftahas/Quantum-Computing/blob/main/variational_quantum_eigensolver.ipynb), and
[`quantum_error_correction.ipynb`](https://github.com/ftahas/Quantum-Computing/blob/main/quantum_error_correction.ipynb).