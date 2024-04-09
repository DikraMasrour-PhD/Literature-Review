---
Reference: "Ronneberger, O., Fischer, P., & Brox, T. (2015). U-Net: Convolutional Networks for Biomedical Image Segmentation. In N. Navab, J. Hornegger, W. M. Wells, & A. F. Frangi (Eds.), Medical Image Computing and Computer-Assisted Intervention – MICCAI 2015 (pp. 234–241). Springer International Publishing. https://doi.org/10.1007/978-3-319-24574-4_28"
Paper Title: "U-Net: Convolutional Networks for Biomedical Image Segmentation"
tags:
  - Architecture
  - Paper
  - ImageSeg
Implemetation: https://github.com/milesial/Pytorch-UNet/
---
 The U-Net architecture comprises two parts, a **contracting path** to capture context, and a symmetric **expanding path** that enables precise localisation. 
> - The down-sampling or contracting path has a VGG-like architecture: 
> 	- **Repeat** ((2 x # of feature maps from previous step x 3x3 unpadded convs + ReLU + 2x2 Maxpool)) 
> - The up-sampling or expansive path uses up-convolution, halving the number of feature maps while increasing their dimensions: this is achieved in code either by 1. combining bilinear interpolation and normal convolutions with half # features or 2. using tranposed convolutions.
> - Feature maps from the contracting path of the network are copied and cropped to the expansive path to avoid losing pattern information (*captures details and localisation*). 
> - Finally, a 1 × 1 convolution processes the feature maps to generate a segmentation map of depth = # of classes
![[unet_arch.png|600]]
