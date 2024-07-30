---
tags:
  - Other
---
- [ ] DenseNets ([see](https://towardsdatascience.com/understanding-and-visualizing-densenets-7f688092391a))
- [ ] Attention mechanism: soft & hard attention
- [ ] Few-shot learning paradigm
- [ ] SNNs: spiking neural networks
- [ ] Dynamic NLP
- [ ] Feature enhancement
- [ ] REINFORCE algorithm
- [ ] Synaptic pruning
- [ ]  MoE - Mixture of Experts
## MoE - Mixture of Experts
### Resources
[Mixture-of-Experts Course: by Geoffrey Hinton](https://www.youtube.com/watch?v=FxrTtRvYQWk|)
[Machine Learning Mastery article](https://machinelearningmastery.com/mixture-of-experts/)
[Wikipedia: Mixture of experts](https://en.wikipedia.org/wiki/Mixture_of_experts#Basic_theory)
![Hu-po stream: From Sparse to Soft Mixture of of Experts](https://www.youtube.com/watch?v=_epq9VsViJc)
### Mixture of experts: what is it?
MoE is an ensemble learning approach that involves dividing the main task (which is often complex) into sub-tasks that 'expert models' specialise in, a 'gating model' then decides which expert model's prediction to trust more based on the input values. Finally, all/some expert models' predictions are combined into one final prediction. 
#### Basic theory
>[!tip] Basic Theory of MoE
>In mixture of experts, we always have the following ingredients, but they are constructed and combined differently.
> 	- There are experts $f_{1}...f_{n}$ each taking in the same input $x$, and produces outputs $f_{1}(x)...f_{n}(x)$ .
> 	-There is a single weighting function (aka gating function) $w$ which takes in $x$ and produces a vector of outputs $(w(x)_1 ... w(x)_n)$
>	- $θ = (θ_0,*θ_1, ..., θ_n)$ is the set of parameters. The parameter $θ_0$ is for the weighting function.
>	- Given an input $x$, the mixture of experts produces a single combined output by combining $f_{1}(x)...f_{n}(x)$  according to the weights $(w(x)_1 ... w(x)_n)$ in some way.
>
>Both the experts and the weighting function are trained by minimising some form of loss function, generally by gradient descent. There is a lot of freedom in choosing the precise form of experts, the weighting function, and the loss function.
### MoE concepts
The MoE approach involves 4 elements
- Divide tasks into sub-tasks
- Develop / Train a specialised expert for each subs task
- Develop a gating model (manager/decision-maker) to decide which expert to use
- Pool predictions based on the gating model's decision
#### Expert models
![[Pasted image 20231128162913.png|400]]
#### Gating model
This model decides on-the-fly the weights to give each expert model's prediction based on the input values.
![[Pasted image 20231128162729.png]]
#### Pooling method(s)
To make a final prediction, the experts' predictions weighted by the gating model's decision are pooled or aggregated:
- Some methods suggest to choose the prediction with the highest confidence score according to the gating model
- Alternatively, a weighted sum of the predictions and the weights given by the gating model can be computed
### Variants of MoE
##### Before Deep Learning
- Meta-pi network
- Adaptive mixture of experts
- Hierarchical MoE
##### Deep Learning MoE
- Sparsely-gated MoE layer
- Routing 
- Capacity factor
#### Cons
> [!failure] Cons of MoE
> - For MoEs to perform well, large data is required

