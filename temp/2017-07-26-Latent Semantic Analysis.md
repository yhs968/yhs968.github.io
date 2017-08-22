---
layout: post
title:  "Latent Semantic Analysis"
date:   2017-07-26
categories: information retrieval
---
# Contents
- Background: Low-rank approximation of a matrix
  - Motivation
  - Frobenius Norm
  - Low-rank approximation
- Latent Semantic Analysis
  - The form of a data matrix
  - Low-rank approximation using SVD
---
# Background:  Low-rank Approximation of a Matrix
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

---
# Latent Semantic Analysis
- Data Matrix
  - $\mathrm{X}$: $v\times d$ term-document matrix
    $$
    \begin{eqnarray}
    \mathrm{X}=
    \begin{bmatrix}
    0 & 1 & 0 & \dots & 2 & 0\\
    13 & 2 & 0 & \dots & 9 & 6\\
    \vdots & \vdots & \vdots & & \vdots & \vdots\\
    7 & 4 & 1 & \dots & 3 & 0
    \end{bmatrix}
    \end{eqnarray}
    $$
    - $\mathrm{X}_{ij}$=the number of times that i-th term appeared in the j-th document.
    - Depending on the context, $\mathrm{X}_{ij}$ might also represent a *[tf-idf](https://nlp.stanford.edu/IR-book/html/htmledition/tf-idf-weighting-1.html)* value or a simple indicator value for whether the i-th term appeared in the j-th document or not. However, how we apply LSA on the data matrix is independent of what $\mathrm{X}_{ij}$ represent.
  - Simple term-document matrix fails to capture *synonymy* and *polysemy*
    - synonymy: different words, same meaning.
    - polysemy: same words, different meaning.
- **Goal of LSA**
  - Utilize the co-occurence information to capture synonymy and polysemy, by projecting frequently co-occuring terms onto the common subspace.
  - Information for two highly (linearly) correlated terms(i.e. two dimension) can be reduced into one **latent** term(dimension).
  - Information for many highly correlated terms can be reduced into one dimension.
- Low-rank approximation using SVD
  $$
  \begin{eqnarray}
  \mathrm{X}\approx\mathrm{X}_k&=&\mathrm{U}_k\Sigma_k\mathrm{V}_k^T\\
  &=&\sum_{i=1}^{k}{\sigma_{i}\mathbf{u}_i\mathbf{v}_i^T}\\
  &=&
  \begin{bmatrix}
  
  \end{bmatrix}
  \end{eqnarray}
  $$