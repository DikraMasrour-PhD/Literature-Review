### Option 1
Autoencoder: reconstruction-trained band selector
- Pretrain band selection module in a reconstruction task
- Freeze band selection module and use for training a segmenting model, model only trained with top-k channels as input
> [!done] Advantages
> - Mask at inference time adapts to the input = dynamic network

> [!fail] Shortcomings
> - Are bands that are easy to reconstruct the image in the reconstruction task necessarily the less useful ones for segmentation?
### Option 2
Segmentation-trained band selector
- Pretrain band selection module in a segmentation task (no pruning)
- Freeze band selector and use for training a less complex segmentation model only on top-k. BackProp not applied to band selector model.
- Knowledge distillation: between 1st segmentation model and 2nd
**Class specialisation**
- Class-specific branches after band selection module that route pixels according to its label during training, and route according to user choice during inference.
> [!done] Advantages
> - Pretraining and training are done on the same task => the selected bands surely match the downstream task
> - Class-specific branches allow for dynamic routing of samples and adjusting mask

> [!fail] Shortcomings
> - At inference time we might load class specific branches that are not going to be used
### Option 3
- Autoencoder: reconstruction-trained band selector
- Extract fixed masks from training on specific classes (fixed mask = topk(average of weights of training samples))
- Reuse fixed masks for inference on specified class
- 1 model = 1 class
> [!done] Advantages
> - Every model is well specialised on the class it was trained on

> [!fail] Shortcomings
> - No dynamicity inside the network, only a dynamic application based on the user's choice
### Common Problems
- **Sparsity**: with L1 norm in loss, does it give enough pronounced sparsity (are the low weights very low and high weights very high?), can we have a constraint that guarantees a minimum number of very high weights?