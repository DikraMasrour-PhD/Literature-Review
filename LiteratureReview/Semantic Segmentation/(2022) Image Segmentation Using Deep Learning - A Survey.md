---
Paper Title: Image Segmentation Using Deep Learning - A Survey
tags:
  - Survey
  - Paper
  - ImageSeg
Reference: "Minaee, S., Boykov, Y., Porikli, F., Plaza, A., Kehtarnavaz, N., & Terzopoulos, D. (2022). Image Segmentation Using Deep Learning: A Survey. IEEE Transactions on Pattern Analysis and Machine Intelligence, 44(7), 3523–3542. https://doi.org/10.1109/TPAMI.2021.3059968"
---
### 2nd draft noted
DL Techniques discussed: 100+ up to 2019 grouped as follows:
1. ~~Fully convolutional networks~~
2. ~~Conv models with graphical models~~
3. ~~Encoder-decoder models~~
4. ~~Multi-scale and pyramid networks~~
5. R-CNN models (for instance segmentation)
6. Dilated conv models & DeepLab family
7. Recurrent NNs
8. Attention-based models
9. Generative models & Adversarial training
10. Conv models with active contour models
11. Other
#### Semantic segmentation: Problem Formulation:
- Pixel classification with semantic labels: Semantic segmentation
- Partitioning of individual objects: Instance segmentation
#### [[(2015) FCN - Fully Convolutional Networks for Semantic Segmentation|FCNs]] for semantic segmentation
- FCNs are able to take an *arbitrarily-sized* input image and produce a *correspondingly-sized* output, as opposed to other CNN architectures (vgg, resnet,...) by reinterpreting the fully connected layers as fully convolutional layers
- FCNs have proven to be especially useful for dense prediction tasks *(e.g. semantic segmentation & object detection)*
- Limitations of FCNs include ignoring of global scene-level context and poor generalisation to 3D images.
#### Convolutional models x [[Fundamentals#Markov Random Field models|Graphical models]]
The main purpose of exploring graphical models is to include more contextual information into the model and improve semantic image segmentation. 
CRFs can be trained separately from neural network or trained jointly.
#### Encoder-Decoder based models
The paper brings up several Encoder-Decoder-based models:
- **DeconvNet** (Noh et al, 2015)
- **SegNet** (Badrinarayanan et al., 2017): its main contribution is to save the max pooling indices to be used in the unpooling operation in the decoder network. Eliminating the need for learning upsampling filters, as in FCN
>> [!warning] This technique seems to have been used in the (Noh et al, 2015) paper too, is it really a novelty?
- **HRNet** (Sun et al., 2019): instead of going down the approach of U-net-like networks of recovering the resolution of the feature maps in the decoder network through upsampling and 'deconvolution' techniques, the authors explore the approach of maintaining high-resolution representation using high-resolution convolution, and strengthening them with parallel low-resolution convolutions. This technique is relevant to semantic segmentation and object detection. The authors present a couple version of the network HRNetV1 (a), HRNetV2 (b), HRNetV2p (c)  
![[hrnet_arch0.png|700]]
*(Figure 1)*
The last 4-resolution feature maps in Figure 1 are the input in the 3 cases in Figure 2
![[HRNet_versions.png|400]]
*(Figure 2)*	
- [[(2015) U-Net Convolutional Networks for Biomedical Image Segmentation|U-Net]] (Ronneberger et al., 2015)
	- **Unet++**: Unet nested variant (Zhou et al, 2018)
- **ResUNet** (Zhang et al, 2018): Combined U-Net & ResNet for a road extraction task on remote sensing images from the Massachusetts Roads dataset
- **V-Net** (Milletari et al., 2016): used for 3D image segmentation. The authors introduced a new ==Dice coefficient-based== objective function
#### Multi-scale and Pyramid Network based models
- [[(FPN) Feature Pyramid Network]] (Lin et al., 2017): bottom-up + top-down + lateral connections. FPNs make use of the inherent hierarchical nature of CNNs to produce predictions at all scales of features.
	![[fpn-arch.png|400]]
- **(PSPN) Pyramid Scene Parsing Network** (Zhao et al, 2017): 
	- Resnet as feature extractor
	- Pyramid pooling module: performs pooling at different scales
	- Pooling results are up-sampled to the initial feature map resolution and concatenated to capture global and local context
	- Conv layers to generate pixel-wise predictions
		![[pspn-arch.png|500]]
- Other models: **Dynamic Multi-scale Filters Network, Context contrasted network and gated multi-scale aggregation, Adaptive Pyramid Context Network (APC-Net), Multi-scale context intertwining (MSCI)**
#### R-CNN based Models (instance segmentation)
- [[R-CNN Family|R-CNN]] and its extensions: 
	- [[R-CNN Family#(2015) Fast R-CNN|Fast R-CNN]]
	- [[R-CNN Family#(2017) Faster R-CNN Towards Real-Time Object Detection with Region Proposal Networks|Faster R-CNN]]
	- [[R-CNN Family#(2017) Mask R-CNN|Mask R-CNN|]]
#### Dilated Convolutional Networks and DeepLab Models
#### Segmentation metrics
[[(2015) FCN - Fully Convolutional Networks for Semantic Segmentation#Evaluation metrics|FCN metrics]]
Dice coefficient $\frac{2*|A\cap B|}{|A|+|B|}$

> [!bug]- Limitations
> - [[#Encoder-Decoder based models|(Enc-Dec)]] The main limitation of encoder-decoder based models is the loss of the fine-grained information due to the loss of the high-resolution representations during encoding. This limitation is however mitigated by HRNets. 

>[!tip]- Challenges & Opportunities
>- More challenging datasets
>- Interpretable deep models
>- Weakly supervised (few-shot learning) and unsupervised learning
>- Real-time inference
>- Memory efficient models

