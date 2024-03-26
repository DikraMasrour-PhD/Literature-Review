---
Paper Title: Learning-Based Optimization of Hyperspectral Band Selection for Classification
Reference: Ayna, C. O., Mdrafi, R., Du, Q., & Gurbuz, A. C. (2023). Learning-Based Optimization of Hyperspectral Band Selection for Classification. Remote Sensing, 15(18), 4460. https://doi.org/10.3390/rs15184460
tags:
  - RemoteSensing
  - Paper
  - BandSelection
---
![[mlbs_arch.png]]
### Summary

#### Band selection network
- The approach consists of learning a band mask starting from a seed vector that is randomly initialised then fed into a Sigmoid function: $σ(V) = S$
- The learned mask is then 'normalised': meaning that only a specific number of elements get selected according to a user-determined sparsity ratio. $N(S)$
- The mask is then 'binarised' by sampling a $U_k$ vector from the uniform distribution, the $U_k$ vector is considered as a thresholding vector where the resulting mask is the boolean response of : $N(S) > U_k$. 
- Since this type operations does not allow for differentiability of the gradient during learning, the authors use a trick by transforming the hard-thresholding boolean operation: $$N(S) > U_k$$ into: $$σ(N(S) - U_k)$$ Thus, resulting in a softened thresholding operation and allowing for differentiability.
- The mask is then multiplied by the hyperspectral input vector, the result is then fed to a downstream pixel classification network. The architecture used by the authors for experimentation is a VGG-like architecture performing 1D convolutions of the masked hyperspectral vector.
- The mask is jointly learned with the downstream network parameters using the following loss function $$argmin_{V,Θ} \frac{1}{K}\sum_{k=1}\sum_{j=1}L(f_Θ(σ_r(N_α(σ_t(V))-U_k)*X_j), l_j)$$
	*where L is the cross-entropy loss*
	