**Fri May 24, 2024**
TASE use case
- Better data: combined Hyspecnet-11k Corine with Global Land Cover. Still some label-level noise but less band-level noise.
- Better HSI-adapted encoder by training it on HSI data for reconstruction task (autoencoder)
- Work towards selecting no more than 10-12 bands.
Band selection research
- Build case against FFS.
- Shift from Forward Feature Selection to Reconstruction-based BS using autoencoder-like architecture. Inspiration from [[BS-Net]] to do spectral reconstruction, but also add spatial reconstruction for more robust band selection, plus validate BS with downstream task. Details of the method have yet to be set.
- Goal being: to prove that our selected bands give same or better performance than hand-selected representative bands while reducing computation costs (energy-wise)
Wild ideas
- Think of a way to have a model that also decides on the number of bands to be selected for specific input (Early Exiting-style)
- Think of how to include [[Contribution Ideas#^physics-informed|physics-informed]] band selection 
**Mon May 27, 2024**
==Meeting Pr Mehdi==
- Reproduce BS-Nets, extract class-specific masks, reuse during inference
**Tue June 04, 2024**
==Meeting Pr Mehdi==
- BS-Nets for average performance mask
- BS-Nets for dynamic mask inference 
	- Options: [[(2020) BS-Nets - An End-to-End Framework for Band Selection of Hyperspectral Image#BS-Nets for Convolve use case#Option 1 rec-seg|reconstruction-segmentation]] and [[(2020) BS-Nets - An End-to-End Framework for Band Selection of Hyperspectral Image#BS-Nets for Convolve use case#Option 2 seg-seg|segmentation-segmentation]]
- Graph reconstruction 
	- Option 1: reconstruct node features
	- Option 2: reconstruct node features and adjacency
	- How to motivate the use of graphs instead of CNNs? Multi-class pixels?