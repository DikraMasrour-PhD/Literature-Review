---
Paper Title: Image Segmentation Using Deep Learning - A Survey
tags:
  - Survey
  - Paper
  - ImageSeg
Reference: "Minaee, S., Boykov, Y., Porikli, F., Plaza, A., Kehtarnavaz, N., & Terzopoulos, D. (2022). Image Segmentation Using Deep Learning: A Survey. IEEE Transactions on Pattern Analysis and Machine Intelligence, 44(7), 3523–3542. https://doi.org/10.1109/TPAMI.2021.3059968"
---
### 1st draft noted
DL Techniques discussed: 100+ up to 2019 grouped as follows:
1. ~~Fully convolutional networks~~
2. ~~Conv models with graphical models~~
3. ~~Encoder-decoder models~~
4. Multi-scale and pyramid networks
5. R-CNN models (for instance segmentation)
6. Dilated conv models & DeepLab family
7. Recurrent NNs
8. Attention-based models
9. Generative models & Adversarial training
10. Conv models with active contour models
11. Other
Semantic segmentation problem formulations:
- pixel classification with semantic labels (semantic segmentation) 
- partitioning of individual objects (instance segmentation)
#### [[(2015) Fully Convolutional Networks for Semantic Segmentation|FCNs]] for semantic segmentation
- FCNs are able to take an *arbitrarily-sized* input image and produce a *correspondingly-sized* output, as opposed to other CNN architectures (vgg, resnet,...) by reinterpreting the fully connected layers as fully convolutional layers
- Proven to be especially useful for dense prediction tasks *(e.g. semantic segmentation & object detection)*
- Limitations of FCNs include ignoring of global scene-level context and poor generalisation to 3D images.
#### Convolutional models x [[Fundamentals#Markov Random Field models|Graphical models]]
The main purpose of exploring graphical models is to include more contextual information into the model  to improve semantic image segmentation. 
CRFs can be trained separately from neural network or trained jointly.
#### Encoder-Decoder based models
The paper brings up several Encoder-Decoder-based models:
- **DeconvNet** (Noh et al)
- **SegNet** (Badrinarayanan et al., 2017): its main contribution is the use of the max pooling indices in the unpooling operation in the decoder network. Eliminating the need for learning upsampling filters as in FCN
>> [!warning] This technique seems to have been used in the (Noh et al) paper, is it really a novelty?
- **HRNet** (Sun et al., 2019): instead of going down the approach of U-net-like networks of recovering the resolution of the feature maps in the decoder network through upsampling and 'deconvolution' techniques, they explore the approach of maintaining high-resolution representation using high-resolution convolution, and strengthening them with parallel low-resolution convolutions. This technique is relevant to semantic segmentation and object detection. The authors present a couple version of the network HRNetV1 (a), HRNetV2 (b), HRNetV2p (c)  
![[HRNet_versions.png|400]]	
- **U-Net** (Ronneberger et al., 2015): the training strategy relies on the use of data augmentation to learn from the very few annotated images effectively. The U-Net architecture comprises two parts, a contracting path to capture context, and a symmetric expanding path that enables precise localization. The down-sampling or contracting part has a FCN-like architecture (*capture general context*). The up-sampling or expanding part uses up-convolution, halving the number of feature maps while increasing their dimensions. Feature maps from the down-sampling part of the network are copied and cropped to the up-sampling part to avoid losing pattern information (*captures details and localisation*). Finally, a 1 × 1 convolution processes the feature maps to generate a segmentation map that categorizes each
![[unet_arch.png]]
>- (Zhang et al.): Combined U-Net & ResNet for a road extraction task on remote sensing images from the Massachusetts Roads dataset
- **V-Net** (Milletari et al., 2016)

#### Dilated Convolutional and DeepLab Models
#### Segmentation metrics
[[(2015) Fully Convolutional Networks for Semantic Segmentation#Evaluation metrics|FCN metrics]]
Dice coefficient $\frac{2*|A\cap B|}{|A|+|B|}$

> [!warning]- Limitations
> - [[#Encoder-Decoder based models|(Enc-Dec)]] The main limitation of encoder-decoder based models is the loss of the fine-grained information due to the loss of the high-resolution representations during encoding. This limitation is however mitigated by HRNets. 

>[!tip]- Challenges & Opportunities
>- More challenging datasets
>- Interpretable deep models
>- Weakly supervised (few-shot learning) and unsupervised learning
>- Real-time inference
>- Memory efficient models

