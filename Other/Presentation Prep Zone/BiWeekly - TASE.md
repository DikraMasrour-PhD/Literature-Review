---
Date: 2024-05-03
tags:
  - "#PresentationPrep"
---
#### Outline
- [x] Experiment setup
	- [x] Quick reminder of the DeepLabV3+ model  for segmentation
	- [x] encoder architectures tested
		- [x] resnet50
		- [x] resnet101
	- [x] dataset
	- [x] Present S&E Blocks (READ PAPER WELL)
		- [x] prep script
		- [x] Explain how it is included in Seg model: Squeeze & Excitation as a band selection method
	- [x] Experiment#1
		- [x] Seg model res 50 - no SE
	- [x] Experiment#2
		- [x] Seg model res 101 - no pruning
	- [x] Experiment#3
		- [x] Seg model res 101 - with SE - with pruning
	- [x] Compare results
		- [x] training results
		- [x] inference results
			- [x] performance (miou, fscore)
				- [x] show some cases
			- [x] profiling (flops, latency, param number, model size)
- [x] Opportunities for improvement
	- [x] aggregate classes
	- [ ] about the use case?
	- [x] Train our own encoder, the one used is pre-trained on ImageNet for an image classification task
		- [x] Prob#1: ImageNet are rgb images, so as we progress deeper into the encoder, the kernels are indeed enough to capture 3 input channels info but not 200+ input channels
		- [x] Prob#2: The pre-training was done for an image classification task, not the most suitable for sem seg
		- [x] Prob#3: HSIs are different from natural images
	- [x] Start with conv layers before SE block
	- [x] Have more than one SE block 
		- [x] Idea: beginning & end of encoder
			- [x] Why? Paper says: beginning SE is usually class agnostic, later SE blocks are more specialised

	- [ ] PREP SCRIPT

### Script
as agreed last time we met we would fix an arch and start improving on it, 
about SE nets, it is something that we brought up a bit earlier in our exploration