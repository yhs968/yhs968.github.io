---
layout: post
title:  "Variational Inference"
date:   2016-05-05
categories: jekyll update
---
<!--Mathjax Config 설정-->
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  jax: ["input/TeX","input/MathML","output/HTML-CSS","output/NativeMML"],
  extensions: ["tex2jax.js", "mml2jax.js", "asciimath1jax.js", "MathMenu.js","MathZoom.js"],
  TeX: {
    extensions: ["AMSmath.js","AMSsymbols.js","noErrors.js","noUndefined.js"],
    equationNumbers: {autoNumber: "AMS"}
  },
  tex2jax: {
    inlineMath: [ ['$', '$'], ['\\(', '\\)'] ],
    displayMath: [ ['$$', '$$'], ["\\[", "\\]"] ],
    processEscapes: true,
  }
});
</script>
<!--Mathjax CDN 사용-->
<script type="text/javascript" async
            src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

## Variational Inference(=Variational Bayes)
---

## Cores
- **WHAT** it is
  - Approximates target distributions(often posteriors) by finding the closest distribution from a family of specific parameterized distributions.<sup>[2]</sup>
  - Transform inference problems into optimization problems, constructing an analytical approximation to the target distribution.
- **WHEN** to use:
  - Approximation to the posterior probability  
  In Bayesian Framework, we need the posterior $$p(z|x)={p(z,x)\over p(x)}$$
  ($$z$$ is the vector of the latent variables, or parameters of interest).This requires the computation of the Bayesian evidence $$p(x)$$. However, this quantity is often intractable, so instead we directly approximate $$p(z|x)$$ by the new distribution 
  $$q(z)$$ from a specific family of parametric distribution you choose.
- **vs MCMC**
  - MCMC is a *stochastic, sampling-based* approximation to the posterior.
  - Variational Inference is a *deterministic, optimization-based* approximation to the posterior.
- **vs EM**<sup><a href="https://en.wikipedia.org/wiki/Variational_Bayesian_methods#Compared_with_expectation_maximization_.28EM.29">Comparison</a></sup>
  - EM can be treated a special case of Variational Inference where the conditional probability $$p(z|x)$$ is computable.(and thus approximation of the posterior is unnecessary) This reduces the *ELBO*(discussed later in this post) into 
  $$E_Z[\log{p(X|Z)}]$$
  .[5]
- **Pros** of Variational Bayes
  - Faster than MCMC methods, in general.
  - Deterministic(estimation has 0 variance, and we always get the same solution.)
- **Cons** of Variational Bayes
  - Suffers from bias<sup>[3]</sup>

---

## Approximating the posterior using Variational Inference

### Mean Field Approximation
- Common practice for Variational Inference
- **Objective**  
Find $$q^*(z)$$ in the family of parametric distribution such that
$$
\begin{eqnarray}
&&q^*(z)=\text{argmin}_{q(z)}KL(q(z)||p(z|x))=\text{argmax}_{q(z)}\mathcal{L}(q(z))\text{, where}\notag\\
&&\mathcal{L}(q(z))\text{, or ELBO(Evidence Lower BOund) is defined as}\notag\\
&&\mathcal{L}(q(z))=E_q[\log{p(z,x)}]-E_q[\log{q(z)}]=E_q[\log{p(x|z)}]-KL(q(z)||p(z))\notag\\
\end{eqnarray}
$$  
and subject to the restriction to ease the computation:
$$
q(Z)=\prod_i{q_i(Z_i)}
$$  
See pg.5 of [5] for further details.  
- **Result**
  - $$q(z)$$ that achieves the dual goal of maximizing the likelihood $$E_q[\log{p(x|z)}]$$ while not deviating too far from the prior
  $$p(z)$$
  ,which *somewhat* corresponds to the goal of the Bayesian analysis.  
  (*Note:potential problem when the prior is weak, a.k.a. dominated by the observations. It seems that the prior is not thrown away even if it is useless or even misleading, in terms of data.*)  
- Steps
  1. Decompose the Bayesian evidence  
  $$
  \begin{eqnarray}
  &&\log{p(X)}=KL(q(z)||p(z|x))+\mathcal{L}(q(z))\notag\\
  &&\text{where }\notag\\
  \end{eqnarray}
  $$
  2. Find the optimal $$q$$ maximizing ELBO(or minimizing the KL divergence)
    - d
    - *Coordinate ascent inference* : iteratively update for each $q_i$
  3. Result
    - *Locally optimal* ELBO, and thus a *locally optimal* analytic variational distribution $$q^*$$.  

### Expectation Propagation
- Alternatve method for Variational Inference

### Applications
- Bayesian Models : Gaussian Mixture, LDA, HMM, ...
- Deep Learning : VAE(Variational Autoencoder)<sup>[4]</sup>

---

### References
[1] https://en.wikipedia.org/wiki/Variational_Bayesian_methods  
[2] https://www.quora.com/What-is-variational-Bayes  
[3] https://www.quora.com/When-should-I-prefer-variational-inference-over-MCMC-for-Bayesian-analysis  
[4] http://arxiv.org/pdf/1312.6114v10.pdf  
[5] Variational Inference - A Review for Statisticians