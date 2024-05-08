---
tags:
  - "#PresentationPrep"
Date: 2024-05-09
---
Cool blog post https://element84.com/demos/hyperspectral
### Overview
>[!bug] LOGOS
>- [x] Add Logos
- [x] Title slide (hsi background)
- [x] Overview slide
- [ ] Introduction
	- [ ] hook : think of a good hook
- [x] Intro to satellite (multispectral, hyperspectral) imagery 
	- [x] cubes,...
	- [x] different ways of exploiting satellite imagery: among which: 
		- [ ] ~~scene classification~~
		- [x] **segmentation**
	- [x] what is image segmentation
		- [x] image example
- [ ] **Transition slide** now, how do we achieve segmentation. One of the tools that have gained popularity lately is deep learning
- [ ] Intro to deep learning
	- [ ] introductory concepts of deep learning
	- [ ] why is deep learning adapted to satellite images?
		- [ ] able to handle high dimensional data
		- [ ] automatic feature extraction
		- [ ] flexibility of representation: able to look at and process the satellite image under different lights (independent pixels, images, graphs, ...)
		- [ ] DL vs Trad seg methods (e.g. thresholding)
			- [ ] give example of clear natural image where trad method would excel and a more complex image where trad fails and DL excels
- [ ] Deep learning for segmentation
	- [ ] List popular architectures
		- [ ] quickly talk about encoder-decoder architecture
- [ ] Challenges
	- [ ] Annotation & labelling 
		- [ ] cost 
		- [ ] precision
- [ ] Applications & Research directions
	- [ ] https://www.viact.ai/post/top-10-applications-of-satellite-imagery-ai
	- [ ] https://www.geospatialworld.net/prime/use-cases-satellite-imagery-across-sectors/
- [ ] Example of indian pines segmentation ??

#### Tell the story
- What is satellite imagery?
	- in the electromagnetic spectrum, there exists wavelengths that go beyond what we can see. these wavelengths reveal more characteristics on materials that we look at. 
	- show electromagnetic spectrum
	- Satellites are equipped with special cameras that are able to capture beyond the visible light 
		- multispectral, hyperspectral
		- difference? show screen record animation
		- so we can look at a multispectral or hyperspectral image as a cube (show cube animation)
	- now, there are different ways to exploit this type of images, one of them is to do segmentation on the contents of these images.
- what is Segmentation 
	- I am sure you came across these cool models that produce this kind of results (show example image of segmentation), so we can define image segmentation as the 'process that divides a digital image into meaningful parts. Imagine you're looking at a photo with your friends. Image segmentation would be like virtually outlining each person in the picture, separating them from the background and potentially from each other. The goal is to group pixels in an image that share similar characteristics together.' This task can be done in different ways (use types here https://mindy-support.com/news-post/what-is-image-segmentation-the-basics-and-key-techniques/)
	- Deep learning
		- now, how do we achieve segmentation. One of the tools that have gained popularity lately is deep learning
			- to put it short **Deep learning** is a type of artificial intelligence inspired by the human brain. It uses artificial neural networks with many layers to ==learn complex patterns from huge amounts of data==, like images or text. Just like the human brain, artificial neural networks can ==automatically discover important features from the high dimensional data==, allowing it to become better at understanding the data they see and tackle ==tasks that were previously difficult for computers==.
			- give example of why deep learning is better suited for satellite images: indian pines dataset how it is difficult to differentiate between types of vegetation??
	- TRANSITION these characteristics happen to be just what we need to process our satellite images (animation of extracting the important phrases)
- Deep learning for segmentation: some of the more popular architecture of deep learning models used for semantic segmentation are unets (quick overview)
- Challenges 
	- all of this is great, but there has to be challenges. and I'll talk to you specifically about one challenge that i personally met during the past few months since I started my PhD
		- **Enough accurately annotated data**
- But as it turns out, research should make opportunities out of challenges and this kind of problems have been among the research directions in the field of satellite imagery processing in general 
	- And this brings us to the applications section (show applications from https://www.viact.ai/post/top-10-applications-of-satellite-imagery-ai)
	- directions of research go towards
		- explanability
		- lost resource processing (edgeAI) that aims at reducing costs and delay by moving all the processing to the 'edge' which in our case is the space mission or drone responsible for collecting the images. 