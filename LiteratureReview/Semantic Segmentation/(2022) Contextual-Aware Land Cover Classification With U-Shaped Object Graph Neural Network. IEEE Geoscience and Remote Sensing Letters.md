---
Reference:
  - Zhao, W., Peng, S., Chen, J., & Peng, R. (2022). Contextual-Aware Land Cover Classification With U-Shaped Object Graph Neural Network. IEEE Geoscience and Remote Sensing Letters, 19, 1–5. https://doi.org/10.1109/LGRS.2022.3177778
Paper Title:
  - Contextual-Aware Land Cover Classification With U-Shaped Object Graph Neural Network
tags:
  - Paper
  - GNN
---
![[ougnn-arch.png|900]]
### Context
- As applied in the paper, the proposed method is tested on RGB aerial images not HSIs for land cover classification
### Graph feature extraction: Self-adaptive graph construction
- With SLIC algo, the superpixel (object) segmentation of the input image is extracted => spectral information ?
- From each object, geometric information is extracted: area, perimeter, and solidity
- INIT: at the start, the graph is constructed by the superpixels (objects) as nodes, the edges are assigned to each object's 1st order neighbours, and the node attributes are the combined spectral and geometric information
#### 1. Adjacent graph construction
**Superpixel segmentation** 
- Using the SLIC algorithm to generate superpixels. 
- SLIC bases the grouping of pixels on k-means clustering using color similarity and spatial proximity of pixels.
- At the output of SLIC, the superpixels are then uniquely ID-ed with an assigned label
**Superpixel node attributes**
- Each superpixel has attributes
	- spectral attributes: rgb
	- geometric attributes: area, perimeter, solidity
- At the output of this step, we still have a feature map of superpixels with their spectral and geometric information assigned to each
#### 2. Feature combination & extraction
- The spectral and geometric features of each superpixel are then fused with
	1. 1x1 Conv  fuses (convolves) the geometric and spectral information of superpixels
	2. Multihead Attention Block
		1. MAB is the concatenation of multiple attention heads on the features resulting from 1x1 Conv layer.
			1. Multiple heads are used for robustness of attention
- The output of this step is 'attended' features of the superpixel map 
#### 3. Adaptive edge generation
- The paper uses the new 'attended' feature map to further explore the relationships between the superpixels by generating edges between nodes that may no be close spatially but semantically similar (thanks to the conv+MAB feature extraction)
- The paper uses the KDAM algorithm to compute similarities between the superpixels and generate new edges where it judges that similarity is high.
	![[sagc-example.png|400]]
- The output of this step is a graph of superpixels (nodes) connected with spatially and semantically similar superpixels, it is also the input to the next part of the model.

![[sagc-algo.png|500]]
*Lines 7-11 represent the KDAM algorithm of similarity computation*
### U-OGNN land cover classification
GATConv step is used to transform the binary adjacency matrix to a weighted adjacency matrix. 
Two main components standout in this part
- **Graph encoder** 
	- Similar to an average pooling operation, in order to abstract new nodes from the previous graph, the graph encoder 
- **Graph decoder**