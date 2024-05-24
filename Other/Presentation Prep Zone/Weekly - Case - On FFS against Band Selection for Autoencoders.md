### FFS Pros & Cons
**pros**
- does band selection
- less complex than deep learning
**cons**
- no more dynamicity of bands: non-input dependent
- ignores inter-relationships between bands which is one of the most important characteristics of HS bands
	- iterative nature of FFS does not allow to consider different band combinations
- too much computation: train 20100 models
- defies the purpose of using Deep learning which inherently is able to do more complex feature selection
- suboptimal
	- if we plan to use a complex DL model, a suboptimal starting point would limit our model's performance 
- is it correct and fair to compare a complex deep CNN with few features, is it a good starting point?
>[!tip]- **Mismatched Approaches:**
>
>- **FFS Goal:** The goal of FFS is to identify the most informative features for a task. It typically starts with a large pool of features and iteratively selects the most relevant ones.
>- **CNN Purpose:** A CNN is designed to automatically learn and extract features from raw data (like images) through its convolutional layers.
>
**Redundancy and Inefficiency:**
>
>- A complex CNN model with many layers and parameters is built to handle high-dimensional data with rich information. Feeding it a single feature essentially bypasses its core functionality of feature extraction.
>- The model would be treating the single feature as if it already contained all the necessary information, making the complex architecture unnecessary and computationally expensive.
>
**Limited Insights:**
>
>- Comparing performance in this scenario wouldn't tell you much about the effectiveness of either approach. The CNN wouldn't have a chance to show its strength in feature learning, and the single feature might not be sufficient for accurate classification.
>
**Alternative Approaches for FFS Stages:**
>
>- **Simpler Models:** During the early stages of FFS with limited features, it's more appropriate to use simpler models like:
>   - **Logistic Regression:** Can handle single features and provides interpretable results about the feature's impact on classification.
> - **k-Nearest Neighbors (kNN):** Effective for low-dimensional data and can provide insights into the feature space.
>- **Feature Engineering:** Focus on exploring additional features that might be more informative for the task. This could involve domain knowledge or feature transformation techniques.	
- what would be the contribution??
- Similar methods have been used in the literature (see BS survey), worth exploring old methods ??
=> ==SPEND TIME ON FFS OR NOT?==
### AE Pros & Cons
**pros**
- input-dependent band selection
- looks at the entire spectrum and able to capture non-linear relationships
- 
### Alt
- BS-Net 
- ''Segmented autoencoder''

### Storyline
- [ ] FFS
	- [ ] pros 
	- [ ] limitations (choose order wisely)
- [ ] Alternative
	- [ ] AE based architecture
	- [ ] Why? advantages over FFS limitations
	- [ ] Present BS Net paper
	- [ ] More to add to BS Net to consider spectral and spatial information by reconstructing the spectral bands and spatial patches of the image
- [ ] Next?
	- [ ] initial simulation and results