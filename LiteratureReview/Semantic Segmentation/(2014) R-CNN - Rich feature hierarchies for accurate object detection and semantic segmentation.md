---
Reference: Girshick, R., Donahue, J., Darrell, T., & Malik, J. (2014). Rich feature hierarchies for accurate object detection and semantic segmentation (arXiv:1311.2524; Version 5). arXiv. https://doi.org/10.48550/arXiv.1311.2524
Paper Title: Rich feature hierarchies for accurate object detection and semantic segmentation
tags:
  - Architecture
  - ImageSeg
  - Paper
---
### Draft 
![[r-cnn-arch.png|600]]
The object detection system consists of 3 modules:
1. **Region proposal** Category-independent region proposals
2. **Feature extraction** Large convolutional network that extracts a fixed-length feature vector from each region
3. **Classification** Set of category-specific classifiers (linear SVMs)
##### 1. Region proposals
To conduct a controlled comparison, the authors opt for the use of Selective Search Algorithm as a region proposal method.
>[!info]- Selective Search
>**Selective Search** is a region proposal algorithm for object detection tasks. It starts by over-segmenting the image based on intensity of the pixels using a graph-based segmentation method by Felzenszwalb and Huttenlocher. Selective Search then takes these oversegments as initial input and performs the following steps
>1. Add all bounding boxes corresponding to segmented parts to the list of regional proposals
>2. Group adjacent segments based on similarity
>3. Go to step 1
At each iteration, larger segments are formed and added to the list of region proposals. Hence we create region proposals from smaller segments to larger segments in a bottom-up approach. This is what we mean by computing “hierarchical” segmentations using Felzenszwalb and Huttenlocher’s oversegments
>Source: [paperswithcode](https://paperswithcode.com/method/selective-search) 
##### 2. Feature extraction
Feature vectors are then extracted from each region proposal using a CNN (Krishevsky et al. Caffe implementation)
The region proposals are usually of arbitrary sizes. Thus the authors opt for dilating the bounding box to include exactly *p* pixels of region, then warping/constraining an arbitrarily shaped region to a fixed-size bounding box