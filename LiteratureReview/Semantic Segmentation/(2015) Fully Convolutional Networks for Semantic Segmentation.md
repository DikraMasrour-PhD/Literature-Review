---
Paper Title: Fully Convolutional Networks for Semantic Segmentation
Reference: Long, J., Shelhamer, E., & Darrell, T. (2015). Fully Convolutional Networks for Semantic Segmentation. 3431–3440. https://openaccess.thecvf.com/content_cvpr_2015/html/Long_Fully_Convolutional_Networks_2015_CVPR_paper.html
Implemetation: https://github.com/shelhamer/fcn.berkeleyvision.org
tags:
  - ImageSeg
  - Paper
  - Architecture
---
## 2nd draft
#### Main contribution
- Casting/interpreting fully **connected** layers that play the role of head-classifier as fully **convolutional** layers, for the purpose of use in semantic segmentation tasks.
- This casting allows for resizing of resulting feature maps back to their original resolution, while being flexible in terms of input size
- **FConn to FConv**: refer to ***Section 4.1. From classifier to dense FCN*** 
- The output of an FCNet is a feature map of the same resolution as the input image, and as many channels as there are classes to predict with pixels values being predictions. Thus, the predicted label for a pixel corresponds to the max probability of predicted values across all channels. 
- **The model outputs a spatial segmentation map instead of classification scores.**
#### Convolution step
Classic convolution blocks. The authors experiment with fine-tuning existing classification nets and building a new FCNet.
#### Deconvolution step
>[!warning] Terminology Alert
>- '*Deconvolution*' in the paper refers to *Transposed convolution* or *Fractionally strided convolution*, which is the operation of upsampling the low-resolution feature maps into higher resolution feature maps. The authors experiment with many ways to do it, and settle with a learned upsampling that is initialised to the parameter of bilinear interpolation.
>- Demystification @[Convolutions: Transposed & Deconvolutions](https://medium.com/@marsxiang/convolutions-transposed-and-deconvolution-6430c358a5b6)
#### Upsampling strategies
###### Shift-and-stitch is filter rarefaction (Sec 3.2)
*Credits: [StackOverflow shift-and-stitch](https://stackoverflow.com/questions/40690951/how-does-shift-and-stitch-in-a-fully-convolutional-network-work)*
![[shift-stitch.png|600]]
- A-trous algorithm utilising wavelets: yields identical results to the shift-and-stitch, less costly.
- Filter enlargement / rarefaction + convolution: to reproduce the shift-and-stitch trick 
> [!info]- Filter rarefaction in CNNs
> - **Standard Convolution:** In a typical convolutional layer within a CNN, filters (or kernels) slide over the input with a specific stride.
> - **Dilated Convolution:** Filter rarefaction introduces "gaps" or spaces within the kernel itself. Consider it like "inflating" the filter with zeros between its values. This is controlled by a parameter called the "dilation rate."
> - For example, a dilation rate of 2 means there's a gap of one zero-value between each element of the filter.
> **Why Do We Use It?**
> 1. **Enlarging the Receptive Field:** Dilated convolutions dramatically increase the receptive field of a filter _without_ increasing the number of parameters (weights) in the network. A larger receptive field means the filter can "see" a wider context of the input image.
> 2. **Capturing Context:** This is crucial in tasks like:
> 		- **Semantic segmentation:** Where you need to understand the context of each pixel for classification.
> Credits: [Google Gemini](https://gemini.google.com/)

> **Conclusion**: The authors do not move forwards with shift-and-stitch trick. As learned upsampling proves to be more effective and efficient.
###### Upsampling is backwards strided convolution (Sec 3.3)
- Bilinear interpolation
>> [!info]- Bilinear interpolation summary
> ![[bilinear_interpolation.png]]
> Source: [CSC320: Introduction to Visual Computing Michael Guerzhoy - University of Toronto](chrome-extension://efaidnbmnnnibpcajpcglclefindmkaj/https://www.cs.toronto.edu/~guerzhoy/320/lec/upsampling.pdf)
- Learned upsampling
	Transposed convolution kernels in the upsampling layers of a FCN do not need to be fixed, but can be learned. 
	>*A stack of deconvolution layers and activation functions can even learn a nonlinear upsampling.* *(Sec3.3)*
	
	>**Conclusion:** The authors settle with learned 'deconvolution' filters, which are initialised with bilinear interpolation weights.
##### Patchwise training is loss sampling (Sec 3.4)
Authors discuss pros and cons of whole-image training (fully convolutional training) VS patchwise training.
>**Conclusion:** the authors opt to use unsampled, whole image training in their experiments *(detailed reasons in Sec 4.3)*
##### Combining what and where (Sec 4.2)
First experiments: 'convolutionising' existing image classification networks, decapitating them of their head-classifier that is replaced by a 1 x 1 x classes convolution, and adding one bilinear upsampling layer to bring the resulting feature map up to the input image resolution. (*Top line upsampling*)
**Results** The final segmentation output is too coarse.
**Solution** Skip connections
###### Skip connections
![[fcn_skip_connection.png]]
> [!example] FCN-16s example 
> - conv7 is the result of the last convolution -> feature map of depth = number of classes
> - upsample the resulting feature map (conv7) 
>- take pool4, convolve it to get a feature map of depth = number of classes
>- concatenate/fuse the corresponding channels with each other(# of channels = # of classes)
>	- the authors say they use Max fusion @ the concatenation step
>- upsample the result of the fusion back to the input image resolution using learned upsampling filters (initialised with bilinear intepolation params)
#### Experiments
The authors conduct experiments on:
- Finer fusion nets: FCN-16 improves mean IU by 3.0 up to **62.4**
- Fusion VS Learned upsampling from last before the last one: fusion wins
- Further fusion & upsampling to FCN-8 improves mean IU to **62.7**
- Beyond FCN-8, the improvements met diminishing returns, so fusion is not done on lower layers.
#### Evaluation metrics
##### Common evaluation metrics for semantic segmentation
<iframe
  src="https://towardsdatascience.com/metrics-to-evaluate-your-semantic-segmentation-model-6bcb99639aa2"
  style="width:100%; height:300px;"
></iframe>

Pixel accuracy ${\sum_{i}n_{ii}}/{\sum_{i}t_i}$
Mean accuracy $\frac{1}{n_{cl}}*\sum_{i}n_{ii}/t_i$
Mean IoU $\frac{1}{n_{cl}}\sum_{i}n_{ii}/(t_i+\sum_{j}n_{ji}-n_{ii})$ = $\frac{|A \cap B|}{|A \cup B|}$ ; 
- IU or IoU : *Intersection over Union* metric
- $n_{ij}$ : *number of pixels of class i predicted to belong to class j*
- *$n_{cl}$ : number of classes*
- $t_i=\sum_{j}n_{ij}$ : *total number of pixels of class i*

Frequency weighted IoU $(\sum_{k}t_k)^{-1}\sum_{i}t_in_{ii}/(t_i+\sum_{j}n_{ji}-n_{ii})$
#### Conclusions & insights
>[!fail] Limitations & critique
>FCNs are considered to be a milestone in semantic segmentation with deep learning but prove not be fast enough for real-time inference, they do not generalise well to 3D image (like HSIs) and do not take global context into consideration efficiently
>ParseNet attempts to solve the global context limitation.

>[!bug] Unclear areas
>- Fully convolutional VS patchwise training: to be detailed
>- Skip connections (fusion step): how is summation of predictions done
>- End-to-end learning of finer-grained networks: *'FCN-16s is learned end-to-end, initialised with the parameters of the last, coarser net, which we now call FCN-32s. The new parameters acting on pool4 are zero-initialised so that the net starts with unmodified predictions.'*
