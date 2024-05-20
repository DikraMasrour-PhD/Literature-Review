---
tags:
  - PresentationPrep
Date: 2024-05-17
---
### Questions to answer
- What does the map of the literature look like?
- What are ways graphs are exploited in image segmentation?
	- it seems that superpixels are used to reduce dimensionality of the amount of data used, especially massive data like images in general and HSIs and SAR specifically. Transforming images into labelled superpixels takes their structure from euclidean data to non-euclidean data, requiring thus, the use of graph representation of the image as they do support non-euclidean data structures over CNNs that are not the best at that.
- Is there one prominent and common way or method?
	- **data representation** superpixels
	- feature extraction CNNs
	- **node clustering** unsupervised
- What do graphs add to traditional segmentation methods? Is it relevant to our case?
	- If we consider the different regions in an image to be nodes (superpixels for example), then the data becomes non-euclidean and harder for CNNs to capture. Graphs model this type of data much better
- Where do CRFs go?
- What are areas of recent research? Do they align with our case?
### Taxonomy (variable)
- [x] Traditional Graph-based methods for image segmentation
- [ ] Deep Learning Graph-based techniques for image segmentation: GNN variants
- [ ] Hybrid Deep Learning techniques for image segmentation: using GNN with other types of models
### Story
- [ ] **Camilus, K. & V K, Govindan. (2012). A Review on Graph Based Segmentation. International Journal of Image, Graphics and Signal Processing. 4. 10.5815/ijigsp.2012.05.01.**  
	<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-goal"><path d="M12 13V2l8 4-8 4"/><path d="M20.561 10.222a9 9 0 1 1-12.55-5.29"/><path d="M8.002 9.997a5 5 0 1 0 8.9 2.02"/></svg> Use paper to list different old methods, and emphasize limitations and future research directions
	- graph cut based methods
		- normalised cut
		- minimum mean cut
		- ratio region
		- isoperimetric algorithm
	- interactive methods: a user intervenes to provide either predefined-points of interest, scribbles to differentiate areas of the image, seed points belonging to different areas (e.g. foreground and background) 
		- interactive graph cut
		- random walker algorithm
		- active contours based graph cut
	- minimum spanning tree methods: mst are leveraged to identify strong connections between nodes (pixels) by removing less significant edges 
	- pyramid based methods: represent images as multi-level resolution graphs based on a reduction factor, one of the pyramid levels is assigned to be the 'working' level in charge of producing the segmentation result
		- regular pyramids
		- irregular pyramids
	- **Insights** these methods struggle to find way into real world and real-time applications for being too costly in terms of computation and time.
- [ ] **Contextual-aware Land Cover Classification with U-shaped Object Graph Neural Network(U-OGNN)**
- [ ] Include fully connected CRFs as a way to improve localisation accuracy in semantic segmentation (coupled with atrous convs) as a post processing step, and how it is very close in intuition to the GNNs premise we are trying to put forward (refer to [[Resources#Comprehensive repos|Prof Maziar Raissi's explanation of CRFs (lecture 26)]])  


