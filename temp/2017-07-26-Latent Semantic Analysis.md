---
layout: post
title:  "Latent Semantic Analysis"
date:   2017-07-26
categories: information retrieval
---
# Contents
## Theories
- Low-rank approximation of a matrix
  - Motivation
  - Frobenius Norm
  - Low-rank approximation
- Latent Semantic Analysis
  - The form of a data matrix
  - Low-rank approximation
## Codes
  - Python
  - Java
---
# Low-rank Approximation of a Matrix
Simply put, a *low-rank approximation of a matrix $\mathrm{X}$* refers to an approximation that yields a low-dimensional representation of $\mathrm{X}$ that can *reconstruct* the original matrix $\mathrm{X}$ well.
Then, what does it mean that an approximation can *reconstruct* the original matrix well?
- *Frobenius Norm* of $\underset{v\times d}{\mathrm{X}}$
$$||\mathrm{X}||_F=\sqrt{\sum_{i=1}^{v}\sum_{j=1}^{d}{X_{ij}^2}}$$
- Objective  
$$\underset{\mathrm{Y}:rank(Y)\le k}{\text{min}}||\mathrm{X}-\mathrm{Y}||_F$$
- SVD  
  The solution to the objective mentioned above is obtained by the *SVD*.  
  Let
  $$\mathrm{X}=\mathrm{U}\Sigma\mathrm{V}^T$$
  the SVD of $\mathrm{X}$.
  Then, using only the top-k columns from $\mathrm{U},\mathrm{V}$, we have
  $$
  \begin{eqnarray}
  \mathrm{X}_k&=&\mathrm{U}_k\Sigma_k\mathrm{V}_k^T\\
  &=&\sum_{i=1}^{k}{\sigma_{i}\mathbf{u}_i\mathbf{v}_i^T}
  \end{eqnarray}
  $$
  It is known that
  $$\mathrm{X}_k=\underset{\mathrm{Y}:rank(Y)\le k}{\text{argmin}}||\mathrm{X}-\mathrm{Y}||_F$$
- Sketch of the low-rank approximation minimizing Frobenius Norm
  - Decompose $\mathrm{X}=\mathrm{U}\Sigma\mathrm{V}^T$ using SVD
  - Use only the top-k columns to obtain $\mathrm{X}_k=\mathrm{U}_k\Sigma_k\mathrm{V}_k^T$