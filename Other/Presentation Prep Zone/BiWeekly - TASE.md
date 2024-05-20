---
Date: 2024-05-03
tags:
  - "#PresentationPrep"
---
#### Outline
- [x] In the continuation of the exploration of more HSI-adapted models: 
	- [x] Ale progress on better data
	- [x] Dikra progress on better backbone segmenter
	- [x] Dikra SE block exploration
- [ ] In terms of Band selection block
	- [ ] ==mitigate non-differentiable gradient: Straight Through Estimator, Gumbel-softmax==
	- [ ] SE with MLP learner ignores the spatial information => Convolutions & Attention instead of GAP & MLP
	- [ ] ==see [[Contribution Ideas#^physics-informed|physics-informed MRI segmentation]]==
- [ ] In terms of Segmentation model
	- [ ] GNN exploration
		- [x] One pattern that emerges is that of using over-segmentation algorithm (SLIC) + CNN for feature extraction + GNN for hidden state computation & segmentation
			- [x] Present **Superpixel-Based Attention Graph Neural Network for Semantic Segmentation in Aerial Images**
				- directed graph of k-nearest neighbours based on euclidean distance
			- [x] Present **Attention Graph Convolution Network for Image Segmentation in Big SAR Imagery Data**
				- convolution on superpixels directly
			- [x] Present [[(2022) Contextual-Aware Land Cover Classification With U-Shaped Object Graph Neural Network. IEEE Geoscience and Remote Sensing Letters]] 
				- adaptive edge generation, not only spatially close nodes are linked but semantically close ones too
		- [x] How does it compare to the rest of literature?
		- [x] Critique, what are good things to take, what are things that can be improved?
			- *Adaptive edge generation* is a pro, inputs a richer graph structure, which is a crucial for a good latent representation of nodes.
			- Otherwise, what do graphs add compared to Convolutions? Neighbourhood-specific processing.
	- [ ] Better adapted CNN
		- [ ] Train encoder from scratch?
	- [ ] Next?

### Outcomes
New combined data:
- less classes 23
- more patches 11k
Encoder pre-training
- no pretrained backbone
- Autoencoder: train unet for encoding input image and decoding the same image
- Then use the encoder for semantic segmentation
=> better performance	
- start with Ale baseline
Autoencoder for band selection, mask some bands and see which are most relevant, have model that selects the number of bands as well.
	- Select 10-12 bands (required in ISS mission)
	- compare learned bands with representative 	ones
Goal: prove that learned bands give better performance than hand-selected ones