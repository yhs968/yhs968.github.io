This document is a collection of materials regarding the field of Topic Modeling, as I progress.
# Early topic models
- LSI(=LSA)
# Probablistic Topic Models
- pLSI
- LDA
- LDA variants
# word-embedding based topic models
- Distributed Representations of Sentences and Documents
  - [Original Paper](https://arxiv.org/pdf/1405.4053.pdf)
  - [Short Explanation(See Example 2)](http://colah.github.io/posts/2015-01-Visualizing-Representations/)

# Hybrid Models
- Gaussian LDA: [paper](http://rajarshd.github.io/papers/acl2015.pdf), [original code](https://github.com/rajarshd/Gaussian_LDA), python code to interpret the results(mine)
- vMF LDA

# Performance Evaluation for Topic Models
- Intrinsic Evaluations
  - [NPMI(Normalized Mutual Information)](https://svn.spraakdata.gu.se/repos/gerlof/pub/www/Docs/npmi-pfd.pdf)
  - Perplexity
    - [How to approximate perplexity for probabilistic topic models](https://www.cs.cmu.edu/~rsalakhu/papers/etm.pdf)
    - [Limitations of Perplexity as a quality measure for topics](https://www.umiacs.umd.edu/~jbg/docs/nips2009-rtl.pdf)
  - [Topic Coherence](http://dirichlet.net/pdf/mimno11optimizing.pdf)
- Extrinsic Evaluations
  - Classification Tasks