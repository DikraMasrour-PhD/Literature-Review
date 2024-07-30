---
tags:
  - BandSelection
  - Experiments
---
## Band (feature) selection

|         Task          |            Dataset             |                                   Bands                                   | Classes |   Model    |        Model details        |                       IoU                        | Fscore  | Avg Latency |  Total FLOPS  | Model size | Number of Params |        Other         | Stopped @ epoch |
| :-------------------: | :----------------------------: | :-----------------------------------------------------------------------: | :-----: | :--------: | :-------------------------: | :----------------------------------------------: | :-----: | :---------: | :-----------: | :--------: | :--------------: | :------------------: | :-------------: |
| Semantic Segmentation | Hyspecnet-11k X Corine dataset |                              224 (all-band)                               |   44    | DeepLabV3+ | Encoder: `resnext50_32x4d`  |   0.5005 (Computed with JaccardIndex Pytorch)    |  ~0.58  |    ~7 ms    | 5 151 752 704 |     -      |        -         | No data augmentation |       69        |
| Semantic Segmentation | Hyspecnet-11k X Corine dataset |                              224 (all-band)                               |   44    | DeepLabV3+ | Encoder: `resnext101_32x8d` |   0.5258 (Computed with JaccardIndex Pytorch)    | ~0.6036 |   ~10 ms    | 9 772 237 312 | 567.04 MB  |       90M        | No data augmentation |       220       |
| Semantic Segmentation | Hyspecnet-11k X Corine dataset |                       50 (S&E + Ranking + Pruning )                       |   44    | DeepLabV3+ | Encoder: `resnext101_32x8d` | 0.49 (Computed with SegModelsPytorch's IoU func) | ~0.7466 |   ~6.7 ms   | 2 920 389 248 | 218.08 MB  |       26M        | No data augmentation |       73        |
| Semantic Segmentation |  Copernicus Global Landcover   | 10 (domain-knowledge)<br>Bands: 10, 20, 30, 40, 50, 60, 70, 100, 150, 200 |   23    |     ?      |              ?              |                        ?                         |  ~0.75  |             |               |            |                  |                      |                 |
|                       |                                |                                full-bands                                 |         |            | Encoder: `resnext50_32x4d`  |                                                  |         |             | 4 862 280 192 | 218.33 MB  |    26,779,175    |                      |                 |
|                       |                                |                                10 (BS-Net)                                |         |            |                             |                                                  |         |             | 2 420 163 840 | 203.53 MB  |    26,182,460    |                      |                 |

