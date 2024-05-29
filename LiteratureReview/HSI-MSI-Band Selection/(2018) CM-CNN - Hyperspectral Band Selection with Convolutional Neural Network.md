---
Reference: Cai, R., Yuan, Y., & Lu, X. (2018). Hyperspectral Band Selection with Convolutional Neural Network. In J.-H. Lai, C.-L. Liu, X. Chen, J. Zhou, T. Tan, N. Zheng, & H. Zha (Eds.), Pattern Recognition and Computer Vision (pp. 396–408). Springer International Publishing. https://doi.org/10.1007/978-3-030-03341-5_33
Paper Title: Hyperspectral Band Selection with Convolutional Neural Network
tags:
  - BandSelection
  - ImageSeg
  - Paper
  - RemoteSensing
---
>***Abstract*** In this paper, a supervised method is proposed based on the ground category with convolutional neural network (CNN). Firstly, we propose a structure called contribution map which can record discriminative feature location. Secondly, the contribution map is added to CNN to generate a new model called contribution map based CNN (CM-CNN). Thirdly, we apply CM-CNN for HSI classification with the whole bands. Then, we can get the contribution map which records discriminative bands location for each category. Finally, the contribution map guides us to select discriminative bands.
#### Summary
**Contribution map** is the weighted sum of the feature maps obtained from the last convolutional layer of the network. The authors make the assumption that the contribution map reflects the importance of each band in the classification task.
The authors use the concept of contribution maps in three different ways:
1. For classification: during training, for each training sample a contribution map can be generated, the contribution map is not to be confused with the resulting vector from the GAP
	![[cmcnn.png|400]]
1. After training, a contribution map can be generated for each class by averaging over all the contribution maps of samples from the same class
2. Generating a general contribution map of bands that are jointly relevant to all classes in the dataset at once. The authors propose 2 methods for selecting this general contribution map from class-wise CMs.
> [!tip] Contribution idea
> Once a contribution map is obtained for each class in the dataset, the authors apply one of 2 methods to select a final contribution map that would apply to all classes at once (one mask for all classes).
> ##### Contribution idea
> Keep the class-wise contribution maps
> Prune les relevant bands from each contribution map based on a threshold (TBD)
> Use the contribution maps dynamically in inference: 
> - decision block that can choose the contribution map accordingly
> - task of classification of a specific class, use corresponding CM ^CMCNN-Contribution


