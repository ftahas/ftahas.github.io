---
layout: post
title: "New repository: numerical evaluation of Fredholm determinants of integrable models"
date: 2024-07-25 16:11:00-0400
inline: false
related_posts: false
---


I have created a new repository for numerically calculation of the field-field correlator of the McGuire model at finite temperatures, check it out [GitHub/ftahas](https://github.com/ftahas/McGuire). 
For the theoretical details on the system, I encourage you to read [arXiv:2202.07657](https://arxiv.org/abs/2202.07657) and [arXiv:2308.06482](https://arxiv.org/abs/2308.06482).
The techniques can be straightforwardly applied to other integrable models.

Firstly, choose the size and the range of the quadrature: 
```bash
gfortran legendre_rule.f90 && ./a.out
```

Then set the systems parameters within the main program and run it:
```bash
gfortran rho_x_exact.f90 && ./a.out
```

And similarly procedures apply to other files. 

Have fun! 
