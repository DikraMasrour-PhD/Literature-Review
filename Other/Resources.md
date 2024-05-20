---
tags:
  - Resource
---
[[#Implementations]]
[[#Comprehensive repos]]
[[#People]]
[[#Datasets]]
[[#Fundamentals]]
[[#Intuitions & Serependities !]]
## Implementations

| Model / Framework | Link                                                      | **`Code framework`** | Paper                                                                            |
| ----------------- | --------------------------------------------------------- | -------------------- | -------------------------------------------------------------------------------- |
| U-Net             | [U-Net Pytorch](https://github.com/milesial/Pytorch-UNet) | **`Pytorch`**        | [[(2015) U-Net Convolutional Networks for Biomedical Image Segmentation\|U-Net]] |

---
## Comprehensive repos

| Repo                                                             | Link                                                                                         | Desc                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |     |
| ---------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --- |
| Doodleverse<br>![[doodleverse_icon.png\|100]]                    | [Doodleverse](https://github.com/Doodleverse)                                                | The doodleverse is an opinionated collection of Python packages designed for geoscientific image segmentation.                                                                                                                                                                                                                                                                                                                                                                                                                                                   |     |
| Satellite-image-deep-learning<br>![[satellite_dl_icon.png\|100]] | [Satellite Image Deep Learning techniques](https://github.com/satellite-image-deep-learning) | The satellite-image-deep-learning organisation provides resources on deep learning applied to satellite and aerial imagery.                                                                                                                                                                                                                                                                                                                                                                                                                                      |     |
| The incredible Pytorch<br>![[the-incredible-pytorch.png\|200]]   | [The Incredible Pytorch](https://github.com/ritchieng/the-incredible-pytorch)                | This is a curated list of tutorials, projects, libraries, videos, papers, books and anything related to the incredible [PyTorch](http://pytorch.org/). Feel free to make a pull request to contribute to this list.                                                                                                                                                                                                                                                                                                                                              |     |
| Applied Deep Learning<br>![[Prof Maziar Raissi.png]]             | [Applied Deep Learning](https://github.com/maziarraissi/Applied-Deep-Learning)               | ==PDF courses & Paper summaries!==<br>This is a two-semester-long course primarily designed for graduate students. However, undergraduate students with demonstrated strong backgrounds in probability, statistics (e.g., linear & logistic regressions), numerical linear algebra and optimization are also welcome to register. We will be pursuing the objective of familiarizing the students with state-of-the-art deep learning techniques employed in the industry. Deep learning is a field that has been witnessing a mini-revolution every few months. |     |

---
##  People

| Title                          | Link                                                              |
| ------------------------------ | ----------------------------------------------------------------- |
| Expert Professor in HS imaging | [Prof. Antonio Plaza](https://sites.google.com/view/antonioplaza) |

---
## Datasets

| Dataset                                 | Quick view                           | Homepage                                                                | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Download                                                                                      |
| --------------------------------------- | ------------------------------------ | ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------- |
| Chikusei Airborne Hyperspectral Dataset | ![[Chikusei.png\|200]]               | https://naotoyokoya.com/Download.html                                   | The hyperspectral dataset has 128 bands in the spectral range from 363 nm to 1018 nm. The scene consists of 2517x2335 pixels and the ground sampling distance was 2.5 m. Ground truth of 19 classes was collected via a field survey and visual inspection using high-resolution color images obtained by Canon EOS 5D Mark II together with the hyperspect                                                                                                                                                                                                                                                                                                                                                                          | [Download on Kaggle](https://www.kaggle.com/datasets/mingliu123/chikusei?resource=download)   |
| Toulouse Hyperspectral Dataset          | ![[toulouse_dataset.png\|300]]       | https://www.toulouse-hyperspectral-data-set.com/                        | The image is provided in ground-level reflectance with **a very high spatial resolution (1 m ground sampling distance) and spectral resolution (< 8 nm) from 0.4 µm to 2.5 µm (310 channels*).** More than **380,000 pixels are sparsely labeled with land cover classes** (and secondarily with land use classes) over an area of 90 km². The land cover nomenclature contains 32 classes hierarchically organized into 16 impermeable surfaces and 16 permeable surfaces as illust                                                                                                                                                                                                                                                 | [Dataset as Module in Python](https://github.com/Romain3Ch216/TlseHypDataSet)                 |
| Aerial Drone Dataset                    | ![[drone_seg.png]]                   | https://www.kaggle.com/datasets/bulentsiyah/semantic-drone-dataset/data | The Semantic Drone Dataset focuses on semantic understanding of urban scenes for increasing the safety of autonomous drone flight and landing procedures. The imagery depicts more than 20 houses from nadir (bird's eye) view acquired at an altitude of 5 to 30 meters above ground. A high resolution camera was used to acquire RGB images at a size of 6000x4000px (24Mpx). The training set 400 public images, the test set 200 private images.<br><br>PERSON DETECTION (bounding box)<br>SEMANTIC SEGMENTATION (pixel annotation)<br>CLASSES tree, gras, other vegetation, dirt, gravel, rocks, water, paved area, pool, person, dog, car, bicycle, roof, wall, fence, fence-pole, window, door, obstacle  obstacle  obstacle | [Download on Kaggle](https://www.kaggle.com/datasets/bulentsiyah/semantic-drone-dataset/data) |
| GID dataset                             | ![[gid-dataset.png]] | https://x-ytong.github.io/project/GID.html                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |                                                                                               |

## Fundamentals
#### Backpropagation
##### Backpropagation in the case of CNNs
[Convolutions and Backpropagation]("https://pavisj.medium.com/convolutions-and-backpropagations-46026a8f5d2c")
#### Markov Random Field models
##### Conditional Random Field Models (CRFs)
[CRFs video](https://www.youtube.com/watch?v=rI3DQS0P2fk)
>[!info]- CRFs summary
>HMM: generative model: models the joint prob between the hidden state and the observed data point (tries to explain how the observed data has been generated in the first place)
CRF:
> - discriminative model: models the conditional prob of hidden state knowing an observed data point : $P(y|X)$
> - not directed graph => more dependencies than HMM
> - supervised: requires labelled data
> - requires a lot of data
>	- Linear chain CRF variant: subset of a CRF that allows specific types of dependencies (only connections between sequential hidden states $Y_{i-1}$ and $Y_i$ ), thus requires less data
>- CRF finds the relationship between an observed data point X and a given hidden state Y == this relationship *f* is called a *feature function*, commonly denoted $Ψ$
>- feature functions can be any function as long as it takes the following inputs  
>	- $X$ : observed data
>	- $Y_{i-1}$ : previous hidden state (assumption of Linear chain CRF)
>	- $Y_i$ : current hidden state
>	- $i$ : index of current hidden state (time step)
>- as many *feature functions* as required can be defined in one CRF
>- a CRF can be trained with SGD to learn the weights $w_j$
>	- let $F(X, Y_{i-1}, Y_{i}, i) = \sum_{j}w_j* f_j(X, y_{i-1}, y_{i}, i)$
>- Back to the end goal:  
>	-  $P(y|X, w) = \frac{1}{Z}e^{\sum_NF(X, Y_{i-1}, Y_{i}, i)}$
>		$Z$ : being the [partition function](https://www.deeplearningbook.org/contents/partition.html) used to normalise the probability distribution 
>	-  $P(y|X, w)$ to be maximised during training
#### Bayesian Deep Learning
[A comprehensive introduction to Bayesian Deep Learning](https://jorisbaan.nl/2021/03/02/introduction-to-bayesian-deep-learning.html)
[A gentle introduction to Bayesian Deep Learning](https://towardsdatascience.com/a-gentle-introduction-to-bayesian-deep-learning-d298c7243fd6)
#### Feature selection 
[Feature selection techniques in Machine Learning](https://www.analyticsvidhya.com/blog/2020/10/feature-selection-techniques-in-machine-learning/)
#### Graph Neural Networks
[Gentle Introduction to Graph Neural Networks](https://distill.pub/2021/gnn-intro/)
#### Graph Signal Processing
[Graph Signal Processing](https://web.media.mit.edu/~xdong/talk/BDI_GSP.pdf)
### Remote Sensing
#### Digital Numbers, Radiance and Reflectance
[Digital Numbers, Radiance and Reflectance](https://www.nv5geospatialsoftware.com/Learn/Blogs/Blog-Details/ArtMID/10198/ArticleID/16278/Digital-Number-Radiance-and-Reflectance)
### Math
#### Calculus
[Betterexplained Calculus](https://betterexplained.com/calculus/)
#### Eigenvalues & eigenvectors
**Intuition of eigenvalues & eignenvectors** [Eigenvalues & eigenvectors: Wikipedia](https://en.wikipedia.org/wiki/Eigenvalues_and_eigenvectors)

## Intuitions & Serependities !

>[!tip]- About numbers of CNN filters from RGB to HSI
>You might not necessarily need to increase the number of filters simply because you're switching from RGB images to hyperspectral images for training a CNN. Here's why:
>- **Focus of Filter Increase:** The number of filters in a CNN layer is primarily determined by the complexity you want the layer to capture in the data. With RGB images, 3 filters are enough because there are 3 color channels (red, green, blue).
>- **Hyperspectral Complexity:** Hyperspectral images have a higher dimension due to the many spectral bands. However, the inherent complexity within each band might not be significantly higher compared to RGB channels.
>**Factors to Consider for Filter Choice:**
>
>- **Task Complexity:** The complexity of the task you're trying to solve with the CNN will influence the number of filters needed. More complex tasks like material classification with subtle spectral differences might benefit from more filters.
>- **Spectral Information Leverage:** If your goal is to leverage the full spectral information of the hyperspectral data, using a larger number of filters, especially in the initial layers, might be helpful for the model to learn relevant features from each band.
>
**Alternative Approaches:**
>
>- **Feature Engineering:** Before feeding the hyperspectral data directly to the CNN, you could explore feature engineering techniques to extract relevant spectral features. This might allow you to use a similar number of filters in the CNN as with RGB images.
>- **Dimensionality Reduction:** Techniques like Principal Component Analysis (PCA) can be used to reduce the dimensionality of the hyperspectral data while preserving most of the relevant information. This can then be fed into a CNN with a similar filter configuration as for RGB images.
>
**Experimentation is Key:**
>
Ultimately, the optimal number of filters for your CNN with hyperspectral data will depend on your specific task, dataset characteristics, and desired model complexity. It's recommended to experiment with different filter configurations and evaluate the model performance to find the best setting.
>
Credits: [Gemini](https://gemini.google.com)

> [!info]- Fourier transform intuition
> Fourier transform is a transform, meaning that it is a mappings from a space to another. Fourier transform goes from the time to the frequency domain. As shown in the animation, a periodic function $f$ can be decomposed to its fundamental component signals using Fourier series.
> ![[Fourier_transform_time_and_frequency_domains.gif]]

> [!example]- Key, Query, and Value based attention in the context of CNNs
> **Scenario:**
Imagine you're building a model to classify different types of clothing in images (e.g., shirts, pants, dresses). A CNN can extract features from an image, but these features might not explicitly highlight the most important regions for clothing classification (e.g., collars, pockets, sleeves).
**Attention Mechanism Integration:**
>1. **Feature Extraction:** Pass the input image through a pre-trained CNN (e.g., ResNet) to obtain a feature map. This feature map captures spatial information about the image, with each channel representing different aspects.
>2. **Linear Projections:** Apply three separate linear transformations to the feature map (F) to generate the key (K), value (V), and query (Q) vectors:
>    - **Key (K):** K = W_k * F, where W_k is a learned weight matrix. K represents the "importance" of each element in the feature map for the classification task.
>  - **Value (V):** V = W_v * F, where W_v is another learned weight matrix. V represents the actual feature information at each location in the feature map.
>  - **Query (Q):** Q = W_q * x_q, where W_q is a learned weight matrix and x_q is a learnable query vector. The query vector can be task-specific or learned during training.
>3. **Attention Scores:** Calculate the attention scores (a_ij) between each element (i) in the query vector (Q) and all elements (j) in the key vector (K). This score indicates how "relevant" a specific feature location (j) is to the current element (i) in the query. A common way to compute the attention score is:
>  - a_ij = softmax( Q^T * K_j )
>4. **Weighted Values:** Multiply the attention scores (a_ij) with the corresponding value vectors (V_j) to obtain weighted value vectors (v_i'):
 >   - v_i' = Σ(a_ij * V_j)
>5. **New Representation:** Concatenate these weighted value vectors (v_i') to form a new feature representation (F'). This representation emphasizes the most relevant features based on the attention scores.  
>6. **Classification:** Pass the new feature representation (F') through additional fully connected layers for classification into different clothing types.
>
>Source: Gemini

