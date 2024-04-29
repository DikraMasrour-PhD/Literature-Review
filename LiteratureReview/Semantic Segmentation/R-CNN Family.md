---
Reference:
  - Girshick, R., Donahue, J., Darrell, T., & Malik, J. (2014). Rich feature hierarchies for accurate object detection and semantic segmentation (arXiv:1311.2524; Version 5). arXiv. https://doi.org/10.48550/arXiv.1311.2524
  - Girshick, R. (2015). Fast R-CNN. 1440–1448. https://openaccess.thecvf.com/content_iccv_2015/html/Girshick_Fast_R-CNN_ICCV_2015_paper.html
  - "Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks"
  - He, K., Gkioxari, G., Dollar, P., & Girshick, R. (2017). Mask R-CNN. 2961–2969. https://openaccess.thecvf.com/content_iccv_2017/html/He_Mask_R-CNN_ICCV_2017_paper.html
Paper Title:
  - Rich feature hierarchies for accurate object detection and semantic segmentation
  - Fast R-CNN
  - "Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks"
  - Mask R-CNN
Lab:
  - UC Berkley
  - Microsoft Research
  - Facebook AI Research
tags:
  - Architecture
  - ImageSeg
  - Paper
Implemetation:
  - https://github.com/rbgirshick/fast-rcnn
---

**Summary** [R-CNN, Fast R-CNN, Faster R-CNN and Mask R-CNN explained](https://blog.paperspace.com/faster-r-cnn-explained-object-detection/)
# (2014) R-CNN - Rich feature hierarchies for accurate object detection and semantic segmentation
#### Proposed method
![[r-cnn-arch.png|600]]
The R-CNN system consists of 3 modules:
1. **Region proposal** Category-independent region proposals
2. **Feature extraction** Large convolutional network that extracts a fixed-length feature vector from each region
3. **Classification** Set of category-specific classifiers (e.g. linear SVMs)
##### 1. Region proposals
To conduct a controlled comparison with other results in the literature, the authors opt for the use of Selective Search Algorithm as a region proposal method.
>[!info]- Selective Search
>**Selective Search** is a region proposal algorithm for object detection tasks. It starts by over-segmenting the image based on intensity of the pixels using a graph-based segmentation method by Felzenszwalb and Huttenlocher. Selective Search then takes these oversegments as initial input and performs the following steps
>1. Add all bounding boxes corresponding to segmented parts to the list of regional proposals
>2. Group adjacent segments based on similarity
>3. Go to step 1
>At each iteration, larger segments are formed and added to the list of region proposals. Hence we create region proposals from smaller segments to larger segments in a bottom-up approach. This is what we mean by computing “hierarchical” segmentations using Felzenszwalb and Huttenlocher’s oversegments
>Source: [paperswithcode](https://paperswithcode.com/method/selective-search) 
>
>**Felzenszwalb and Huttenlocher (FH) Algorithm** This algorithm, proposed by Pedro Felzenszwalb and Daniel Huttenlocher, is a popular choice for oversegmentation in selective search. It represents the image as a graph where:
>- **Vertices:** Correspond to individual pixels in the image.
>- **Edges:** Connect neighboring pixels and are weighted based on the similarity between those pixels.
**Similarity Measure:**
The weight of an edge connecting two pixels is determined by a similarity measure. This measure considers factors like:
>- **Color difference:** The absolute difference in intensity values between corresponding color channels (red, green, blue) of the two pixels.
>- **Texture difference:** Local variations in intensity values within a small neighborhood around each pixel. This can be measured using statistical properties like standard deviation or entropy.
**Segmentation Process:**
>1. **Initial Graph:** The algorithm starts with a fully connected graph, where every pixel is connected to its neighbors (up to 4 or 8 neighboring pixels depending on the implementation).
>2. **Minimum Spanning Tree (MST):** It then constructs a minimum spanning tree (MST) of the graph. An MST is a subset of edges that connects all vertices with the minimum total edge weight. This essentially creates a collection of small, highly similar pixel clusters.
>3. **Edge Cutting:** The algorithm iteratively removes edges from the MST, starting with the one with the highest weight. Whenever an edge is removed, it effectively separates the two previously connected pixel clusters, resulting in more and more oversegmented regions.
>4. **Thresholding:** The process of removing edges continues until a stopping criterion is reached. This criterion could be:
>	- A pre-defined threshold on the weight of the next edge to be removed.
>	- A desired number of final segments in the image.
##### 2. Feature extraction
Feature vectors are then extracted from each region proposal using a CNN (Krishevsky et al. Caffe implementation)
The region proposals are usually of arbitrary sizes. Thus the authors opt for dilating the bounding box to include exactly *p* pixels in each region, then warping/constraining the result (an arbitrarily shaped region) to a fixed-size bounding box to be fed to the feature extractor.
#### Test time
1. Selective search (in 'fast mode') is run on the test image to extract around 2K region proposals
2. Region proposals are then warped and fed into CNN feature extractor
3. Computed features for each region proposal are then scored using a set of SVM classifiers trained for each class
4. In post-processing, Greedy non-maximum suppression (Greedy NMS) is used to merge regions that belong to the same category by rejecting regions that have higher IoU with other categories
>[!warning] Remark
>In R-CNN, all region proposals are fed to the model (feature extractor + classifiers) one by one. With 2K region proposals generated per image by the selective search algorithm, it can quickly become computationally and time expensive.
# (2015) Fast R-CNN

![[fast-rcnn-arch.png|500]]
As opposed to R-CNN, Fast R-CNN takes as input the whole image and a set of region proposals/regions of interest (RoI) also produced by the Selective Search algorithm.
- The image is first processed through a deep CNN + pooling
- The RoIs defined as a four-tuple -*(r, c, h, w); (r, c): top-left corner coordinates and (h, w): height and width*- are projected into the feature map resulting from the CNN
- The projected RoIs are each pooled using a RoI Pooling layer and passed through FC layers that branch into:
	- **Softmax layer** that estimated the probability over the classes
	- **Bounding-box regressor** that produces the bounding-box positions of the instance
>[!info]- RoI Pooling layer
>**Region of Interest Pooling**, or **RoIPool**, is an operation for extracting a small feature map (e.g., 7×7) from each RoI in detection and segmentation based tasks. Features are extracted from each candidate box, [...]
>The actual scaling to, e.g., 7×7, occurs by dividing the region proposal into equally sized sections, finding the largest value in each section, and then copying these max values to the output buffer. In essence, **RoIPool** is [max pooling](https://paperswithcode.com/method/max-pooling) on a discrete grid based on a box.
>Credits: [paperswithcode](https://paperswithcode.com/method/roi-pooling)


>[!warning] more details: to be continued
# (2017) Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks
![[faster-rcnn-arch.png|300]]
Faster R-CNN improves on Fast R-CNN by replacing the method used to generate region proposals. Instead of using a slow and non-adapted method (selective search), a learnable Region Proposal Network (RPN) is used.
Before reaching the RPN, the input image is fed through a deep CNN. Its resulting feature map is what is fed to the RPN.
**RPN** as in the paper:
- is a fully convolutional network
- takes an arbitrarily sized input image and outputs a set of rectangular object proposals, each with an objectness score
- relies on anchors and sliding windows to generate region proposals:
	- **Anchors** are regularly placed points on the input image. They indicate the center of the **sliding window**.
	- At each sliding window position, *k* region proposals are predicted. They constitute the features of the sliding window at that position. In the paper, 3 scales and 3 aspect ratios are used, thus *k=9*
	- These features are mapped into a lower dim feature (through an intermediate CNN: e.g. VGG)
	- The result is then fed into 2 sibling layers
	
>>> - *regression layer* of depth *4k* outputs encoding the coordinates of the *k* bboxes for the sliding window position in question
>>> - *classification layer* of depth *2k* that estimates the probability of *object* or not for each proposal.
> ![[faster-rcnn-rpn.png|400]]	
> 
- For each sliding window of dimensions $H*W$ we get $H*W*k$ anchors in total 
The rest of the classification and bbox estimation is done identically to the Fast R-CNN
>[!warning] details about fine-tuning, training and shared conv layers: to be continued
# (2017) Mask R-CNN
Mask R-CNN extends on Faster R-CNN by adding to the 2 - classification and bbox-  outputs a third one, that is the object mask.