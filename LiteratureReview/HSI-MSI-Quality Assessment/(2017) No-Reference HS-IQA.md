---
tags:
  - Paper
  - IQA
  - RemoteSensing
Paper Title: No-Reference Hyperspectral Image Quality Assessment via Quality-Sensitive Features Learning
Reference: Remote Sensing | Free Full-Text | No-Reference Hyperspectral Image Quality Assessment via Quality-Sensitive Features Learning,Yang, J., Zhao, Y., Yi, C., & Chan, J. C. W. (2017)
---
#### Summary
The paper aims at assessing the quality of HS images without the need for clean reference images. The authors do that by computing 5 statistical quality-sensitive features from the pristine and distorted HSIs and compare them to assess the HSI quality. 

> [!note] About the no-reference assessment
> Reference-based quality assessment requires to have the clean images and their own distorted or degraded version to be able to evaluate the quality. This is used in compression evaluation for example.
> No-reference assessment however, even though needs 'training' on very few pristine images, is able to evaluate a new image quality based on statistical features common to most images
#### Distortions
- Gaussian noise with sd=0.05
- Gaussian noise with sd=0.20
- Blurring 3x3a average filtering
- Blurring 5x5 average filtering
#### Statistical Quality-sensitive features
![[Pasted image 20231127144037.png|500]]
![[Pasted image 20231127144056.png|500]]
##### Spectral-domain features
1. **Local Spectra normalisation**
	The authors observe that locally normalised spectra of pristine HSIs follows a Gaussian distribution, while the distorted HSIs' normalised spectra deviates from this distribution distinctively. 
	- Local spectra normalisation of an HSI $∈ R^M×^N×^L)$ is done as follows:
			![[Pasted image 20231204170101.png|200]]
			$λ$ is the spectral coordinate $λ={1, 2, ..., L}$, in other words the wavelengths used to capture the HSI
			$μ(λ)$ and $σ(λ)$ are the mean and the std variance
			
> [!tip] Local spectra
> A pixel spectra in a hyperspectral image is a vector of values that describe the intensities at a location (x, y) for z different bands
> See for more: [Pixel spectra explanation](https://www.mathworks.com/help/images/getting-started-with-hyperspectral-image-analysis.html)  

**Extract distribution features from HSIs: shape and scale params**
	![[Pasted image 20231117114211.png|550]]
	To show that the extracted features are sensitive to the image quality
	![[Pasted image 20231117115042.png|400]]
##### Spatial-domain features
1. **Panchromatic images**
	HSIs usually have a large number of spectral bands. For time optimisation's sake, the authors synthesise the HSI into panchromatic (gray-scale/that reflects brightness of pixels) images. Which are useful for bringing forward the textural properties of an image:
	![[Pasted image 20231117120641.png|200]]
	$I$: is the spectral bands corresponding to red, green, blue
	$w$: is the weights assigned to each band 
	The panchromatic image is then locally normalised (the pixel brightness is normalised).
	The pristine HSI do follow a GGD and the distorted ones deviate
	**= Extract distribution features from the HSIs: shape and scale params**
	![[Pasted image 20231117121550.png|500]]
	- **Log-Gabor filter on panchromatic image**
		To exploit the textural properties of the panchromatic image, the authors apply the Log-Gabor filter to the panchromatic image. Again, different distortions lead to different deviated Gaussian distribution, while the pristine one follows a GGD.
		(Same process)
		**= Extract distribution features from the HSIs: shape and scale params**
		![[Pasted image 20231117130018.png|600]]
	- **Directional gradient of Log-Gabor's response map**
		To further exploit the response features of the Log-Gabor filter, the authors exploit the directional gradient of the response map: the vertical gradient.
		(Same process)
		**= Extract distribution features from the HSIs: shape and scale params**
		![[Pasted image 20231117130632.png|600]]
	- **Gradient magnitude of the Log-Gabor's response map**
		This time, the gradient magnitude of the pristine HSIs follows a Weibull distribution and is deviated for distorted images as well
		**= Extract distribution features from the HSIs: shape and scale params**
		![[Pasted image 20231117130853.png|600]]
##### Proof of Parameter Sensitivity to image quality
![[Pasted image 20231117131055.png|500]]
#### Methodology
- Each of the aforementioned features are extracted from the different spectral and spatial properties of the image blocks and fitted to their corresponding distributions: GGD or Weibull
- Each feature vector is a representation of an image block
- The feature vectors are then concatenated into a feature matrix that represents the whole image
- During training:
	- The dimension of the feature matrix is reduced using PCA and a projection matrix is 'learned' as a result
	- Then, the new features are fitted to a Multivariate Gaussian Model and the mean & covariance params are extracted
- During testing:
	- The same steps are applied to the test feature matrix and the pre-learned projection matrix is used for PCA this time
- A distance between the two MVGs' parameters (mean & covariance) is computed and used as the image quality assessment. The distance is a **Bhattacharyya-like** distance proposed in (Mittal et al., 2013)
#### Experiments & Settings
##### Data
In their experiments the authors used 2 datasets:
- AVIRIS sensor data (Moffett Field, Cuprite, Lunar Lake, Indian Piens)
- HyperspecVC sensor data (Chikusei, Ibaraki, Japan)
##### Experiments
###### 1. Comparison to reference-based indices
The proposed ILNIQE is consistent with chosen reference-based metrics
![[Pasted image 20231127143253.png|500]]
###### 2. Spectral feature evaluation
The proposed score is consistent with the SAM(spectral angle mean) index except on the Chikusei2 data, which is explained by the low number of training samples existing in that dataset
![[Pasted image 20231127143408.png|500]]
###### 3. Separate spatial features evaluation
- The Log-Gabor filter feature is the most efficient individually, which is expected thanks to the Log-Gabor filter's ability to extract textures, edges and details
- The spatial features are not optimal when used individually as quality criteria
![[Pasted image 20231127143719.png|500]]
###### 4. Robustness: Cross-dataset evaluation 
Even with the big difference between training and test datasets in terms of image size and resolution, the model is still consistent with reference-based scores and robust across datasets
![[Pasted image 20231127143700.png|500]]
#### Critique / Insights
- How come pristine images features are not clustered in most spatial quality-sensitive features graphs (fig10-12)?
- **Statistical method might be too rigid for downstream tasks that are based on Deep learning, and require many assumptions that might not be present in random real-world data**
#### Related papers
- Zhang, L., Zhang, L., & Bovik, A. C. (2015). A Feature-Enriched Completely Blind Image Quality Evaluator. _IEEE Transactions on Image Processing_, _24_(8), 2579–2591. [https://doi.org/10.1109/TIP.2015.2426416](https://doi.org/10.1109/TIP.2015.2426416)
- Mittal, A., Soundararajan, R., & Bovik, A. C. (2013). Making a “Completely Blind” Image Quality Analyzer. _IEEE Signal Processing Letters_, _20_(3), 209–212. [https://doi.org/10.1109/LSP.2012.2227726](https://doi.org/10.1109/LSP.2012.2227726)