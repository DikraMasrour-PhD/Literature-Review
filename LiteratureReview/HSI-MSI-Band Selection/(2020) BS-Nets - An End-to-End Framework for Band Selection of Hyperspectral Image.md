---
Reference:
  - "Cai, Y., Liu, X., & Cai, Z. (2020). BS-Nets: An End-to-End Framework for Band Selection of Hyperspectral Image. IEEE Transactions on Geoscience and Remote Sensing, 58(3), 1969–1984. https://doi.org/10.1109/TGRS.2019.2951433"
Paper Title:
  - "BS-Nets: An End-to-End Framework for Band Selection of Hyperspectral Image."
tags:
  - BandSelection
  - Paper
---
### Abstract
- many of existing band selection methods separately estimate the significance for every single band and cannot fully consider the nonlinear and global interaction between spectral bands.
- assuming that a complete HSI can be reconstructed from its few informative bands, a framework: band attention module (model the nonlinear inter-dependencies) + reconstruction network
- allows to accurately select informative bands with less redundancy and better classification performance
### Related work
- search, clustering, raking based methods that exist
- searching: time-consuming
- clustering: assume spectral bands are clusterable and look at bands independently ignoring complex relationships
- ranking: band significance independently 
### Method
- BAM: to pay attention to those informative bands and moreover to avoid the influence of the trivial bands.
- **architecture** BAM + RecNet ![[bs-net-arch.png]]
- reconstruction loss used: MSE 
	![[bs-net-loss1.png|200]]
- for sparse band selection they use the l1 norm to force sparsity
	![[bs-net-loss2.png|400]]
- informative bands at the end of training are selected based on their average weight over training samples
- remarks: easy to combine with other tasks and networks, spectral and spatial, captures non-linear relationships
- results compared to other search, rank, cluster based methods![[bs-net-results.png]]