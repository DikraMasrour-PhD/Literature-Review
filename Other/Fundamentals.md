---
tags:
  - Fundamentals
---
# Machine Learning / Deep Learning
## Backpropagation
### Backpropagation in the case of CNNs
[Convolutions and Backpropagation]("https://pavisj.medium.com/convolutions-and-backpropagations-46026a8f5d2c")
## Markov Random Field models
### Hidden Markov Models x Conditional Random Field Models (CRFs)
![CRFs](https://www.youtube.com/watch?v=rI3DQS0P2fk)
HMM: generative model: models the joint prob between the hidden state and the observed data point (tries to explain how the observed data has been generated in the first place)
CRF: 
- discriminative model: models the conditional prob of hidden state knowing an observed data point : $P(y|X)$
- not directed graph => more dependencies than HMM
- supervised: requires labelled data
- requires a lot of data
	- Linear chain CRF variant: subset of a CRF that allows specific types of dependencies (only connections between sequential hidden states $Y_{i-1}$ and $Y_i$ ), thus requires less data
- CRF finds the relationship between an observed data point X and a given hidden state Y == this relationship *f* is called a *feature function*, commonly denoted $Ψ$
- feature functions can be any function as long as it takes the following inputs  
	- $X$ : observed data
	- $Y_{i-1}$ : previous hidden state (assumption of Linear chain CRF)
	- $Y_i$ : current hidden state
	- $i$ : index of current hidden state (time step)
- as many *feature functions* as required can be defined in one CRF
- a CRF can be trained with SGD to learn the weights $w_j$
	- let $F(X, Y_{i-1}, Y_{i}, i) = \sum_{j}w_j* f_j(X, y_{i-1}, y_{i}, i)$
- Back to the end goal:  
	-  $P(y|X, w) = \frac{1}{Z}e^{\sum_NF(X, Y_{i-1}, Y_{i}, i)}$
		$Z$ : being the [partition function](https://www.deeplearningbook.org/contents/partition.html) used to normalise the probability distribution 
	-  $P(y|X, w)$ to be maximised during training
## Bayesian Deep Learning
[A comprehensive introduction to Bayesian Deep Learning](https://jorisbaan.nl/2021/03/02/introduction-to-bayesian-deep-learning.html)
[A gentle introduction to Bayesian Deep Learning](https://towardsdatascience.com/a-gentle-introduction-to-bayesian-deep-learning-d298c7243fd6)
## Feature selection 
[Feature selection techniques in Machine Learning](https://www.analyticsvidhya.com/blog/2020/10/feature-selection-techniques-in-machine-learning/)
# Remote Sensing
## Digital Numbers, Radiance and Reflectance
[Digital Numbers, Radiance and Reflectance](https://www.nv5geospatialsoftware.com/Learn/Blogs/Blog-Details/ArtMID/10198/ArticleID/16278/Digital-Number-Radiance-and-Reflectance)
