# Felipe Taha Sant'Ana

**Theoretical physicist · integrable models, interacting quantum systems, and the occasional orbit of Mercury**

This repository is the source of my personal website, [ftahas.github.io](https://ftahas.github.io/): publications, a CV, lecture notes, and a blog where I work through pieces of physics by computing them.

> *We are all Earthlings.*

## Who I am

I am a physicist at the Federal University of ABC (Brazil), where I am a Visiting Professor. My work is on **interacting quantum systems in reduced dimensionality**: one-dimensional Bose gases, the Lieb–Liniger and Tonks–Girardeau models, mobile impurities at finite temperature, Tan's contact, spin chains and their entanglement, and the integrable field theories that make all of this exactly solvable.

The road to ABC went through

- **University of Salerno** (2024–2025), researcher: density-functional theory and machine learning for conformal-field-theory models.
- **Institute of Physics, Polish Academy of Sciences**, Warsaw (2022–2024): Assistant Professor and NCN Polonez Bis / Marie Skłodowska-Curie Fellow, principal investigator of **CIQS**, *Correlation aspects of Interacting Quantum Systems in reduced dimensionality*.
- **University of Warsaw** (2020–2022): postdoc in Miłosz Panfil's group on dynamic correlation functions of quantum integrable models, in and out of equilibrium.
- **Université Côte d'Azur**, Nice (2018–2019): doctoral stay under a CAPES/COFECUB collaboration.
- **University of São Paulo**, São Carlos: Ph.D. in Physics (2020) on bosons in optical lattices and the one-dimensional interacting Bose gas, M.Sc. in Electrical Engineering (2015) on collision-probability estimation for autonomous robots, and B.Sc. in Physics (2012).

Along the way I have been a quantitative analyst, an AI developer for a robotics team, and a lecturer in quantum field theory, statistical physics, quantum mechanics and computational physics. The common thread is the same: take a system seriously enough to compute it.

## What is on the site

- **[Publications](https://ftahas.github.io/publications/)**: papers on Tan's contact and its large-*N* scaling, mobile impurities in one-dimensional gases, two-spinon effects in the thermal Tonks–Girardeau gas, entanglement asymmetry in the XYZ chain, the lattice nonlinear Schrödinger equation, and perturbation theory for lattice bosons. Also on [Google Scholar](https://scholar.google.com/citations?user=MEW2IXAAAAAJ) and [ORCID](https://orcid.org/0000-0003-0802-9919).
- **[Blog](https://ftahas.github.io/blog/)**: physics done by hand and by code. Recent posts:
  - [Newton vs Einstein in the solar system](https://ftahas.github.io/blog/2026/gravsim-newton-vs-einstein/): a simulator that integrates the planets with Newtonian gravity and with General Relativity and recovers Mercury's 43″ per century, light bending, the Shapiro delay and the small effects that compete with GR. Code at [ftahas/gravsim](https://github.com/ftahas/gravsim).
  - [Quantum theory of scattering by a central potential](https://ftahas.github.io/blog/2026/quantum-scattering-d-dimensions/) in *d* dimensions.
  - [Quantum computing simulations with Qiskit](https://ftahas.github.io/blog/2026/quantum-computing/): gates, entanglement, Grover, phase estimation, Shor, VQE, QAOA and error correction, all simulated classically.
  - [ER = EPR](https://ftahas.github.io/blog/2026/er-epr/), [Black holes](https://ftahas.github.io/blog/2026/black-holes/), [Bose–Einstein condensation](https://ftahas.github.io/blog/2025/bose-einstein-condensate/), [General relativity](https://ftahas.github.io/blog/2025/general-relativity/), the [Ising model](https://ftahas.github.io/blog/2025/ising-model/), the [Lorenz attractor](https://ftahas.github.io/blog/2025/lorenz-attractor/), the [Riemann hypothesis](https://ftahas.github.io/blog/2024/riemann-zeta/), the [Black–Scholes equation](https://ftahas.github.io/blog/2026/black-scholes/), and one [bishop sacrifice in the Italian Game](https://ftahas.github.io/blog/2026/chess-bishop-sacrifice/).
- **[Projects](https://ftahas.github.io/projects/)** and **[CV](https://ftahas.github.io/cv/)**: the CIQS project, teaching, and lecture notes on the Riemann zeta function and on scattering theory.

## Code

Most of the computational side of my work is public on [GitHub](https://github.com/ftahas): [gravsim](https://github.com/ftahas/gravsim) (Newton vs GR in the solar system), [Quantum-Computing](https://github.com/ftahas/Quantum-Computing), [Tonks-Girardeau](https://github.com/ftahas/Tonks-Girardeau), [McGuire](https://github.com/ftahas/McGuire), computational-physics course material, and data-science notebooks. Languages of choice: Python, Julia, Fortran and C/C++, with Mathematica and LaTeX never far away.

## Contact

- Email: [ftahas@proton.me](mailto:ftahas@proton.me)
- LinkedIn: [ftsantana](https://www.linkedin.com/in/ftsantana)
- GitHub: [@ftahas](https://github.com/ftahas)

## About this repository

The site is built with [Jekyll](https://jekyllrb.com/) on the [al-folio](https://github.com/alshedivat/al-folio) theme (MIT licence, see `LICENSE`) and deployed with GitHub Pages. Posts live in `_posts/`, publications in `_bibliography/papers.bib`, the CV in `_data/cv.yml`, and images in `assets/img/`. To preview locally:

```bash
docker compose -f docker-compose-slim.yml up   # http://localhost:8080
```
