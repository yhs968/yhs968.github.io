---
layout: post
title:  "Latent Semantic Analysis"
date:   2017-07-26
categories: information retrieval
---
# Finding similar documents
Suppose you have collected tons of e-books. One day, a friend of yours presented you a .
# Latent Semantic Analysis
## Term-Document Matrix
Now that we have a document, we somehow need to express the documents succinctly, so that machines can process
## Theoretical background: SVD
Let $X$ a $V\times D$ term-document matrix. Then, the term matrix can be decomposed, using **Singular Value Decomposition**, as follows:
$$X=U\Sigma V^T$$
where
1. $U$ is the matrix whose columns are the eigenvectors of $XX^T$
2. $\Sigma$ is the matrix that has the <u>square roots</u> of the eigenvalues(referred to as *singular values*) as its diagonal elements corresponding to the each eigenvectors in $U$, where
3. $V^T$ is the
