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
- **architecture** BAM + RecNet ![[bs-net-arch.png|800]]
- reconstruction loss used: MSE 
	![[bs-net-loss1.png|200]]
- for sparse band selection they use the l1 norm to force sparsity
	![[bs-net-loss2.png|400]]
- informative bands at the end of training are selected based on their average weight over training samples
- remarks: easy to combine with other tasks and networks, spectral and spatial, captures non-linear relationships
- results compared to other search, rank, cluster based methods
	![[bs-net-results.png|800]]
### BS-Nets for Convolve use case
#### Option 1 ^rec-seg
Autoencoder: reconstruction-trained band selector
- Pretrain band selection module in a reconstruction task
- Freeze band selection module and use for training a segmenting model, model only trained with top-k channels as input
> [!done] Advantages
> - Dynamic mask that is input-dependent

> [!fail] Shortcomings
> - Are bands that are easy to reconstruct the image in the reconstruction task necessarily the less useful ones for segmentation?
#### Option 2 ^seg-seg
Segmentation-trained band selector  
- Pretrain band selection module in a segmentation task (no pruning)
- Freeze band selector and use for training a less complex segmentation model only on top-k. BackProp not applied to band selector model.
- Knowledge distillation: between 1st segmentation model and 2nd which will be smaller than the teacher segmentation network
> [!done] Advantages
> - Pretraining and training are done on the same task => the selected bands surely match the downstream task
> - Dynamic mask that is input-dependent

> [!fail] Shortcomings
> - At inference time we might load class specific branches that are not going to be used
#### Option 3
- Autoencoder: reconstruction-trained band selector, reconstruction is guided by the desired class: the loss only considers the pixels of the class
- Extract fixed masks from training on specific classes (fixed mask = topk(average of weights of training samples))
- Reuse fixed masks for inference on specified class
- 1 model = 1 class
> [!done] Advantages
> - Every model is well specialised on the class it was trained on

> [!fail] Shortcomings
> - No dynamicity inside the network, only a dynamic application based on the user's choice
> - Reconstruction is guided by the dataset classes, it is not possible to use a different dataset for reconstruction pre-training and another one for the downstream task
> => Use the same dataset for reconstruction training and downstream task
#### Common Problems
- **Sparsity**: with L1-norm in loss, does it give enough pronounced sparsity (are the low weights very low and high weights very high?), can we have a constraint that guarantees a minimum number of very high weights?
#### Bonus
**Class specialisation**
- Class-specific branches after band selection module that route pixels according to its label during training, and route according to user choice during inference.