## Turn 1 — document page 14 (rank 1 of 20)

Table 3: Contrastive learning settings on MedMNIST and CIFAR-10-LT.
(a) MedMNIST pre-training
| config | value |
|---|---|
| backbone | ResNet-50 |
| optimizer | SGD |
| optimizer momentum | 0.9 |
| weight decay | 1e-4 |
| base learning rate† | 0.03 |
| learning rate schedule | cosine decay |
| warmup epochs | 5 |
| epochs | 200 |
| repeated sampling [21] | see Table 5 |
| augmentation | see Table 4 |
| batch size | 4096 |
| queue length [15] | 65536 |
| τ (equation 1) | 0.05 |

(b) CIFAR-10-LT pre-training
| config | value |
|---|---|
| backbone | ResNet-50 |
| optimizer | SGD |
| optimizer momentum | 0.9 |
| weight decay | 1e-4 |
| base learning rate† | 0.03 |
| learning rate schedule | cosine decay |
| warmup epochs | 5 |
| epochs | 800 |
| repeated sampling [21] | none |
| augmentation | see Table 4 |
| batch size | 512 |
| queue length [15] | 4096 |
| τ (equation 1) | 0.05 |

Pre-training Settings. Our settings mostly follow [15, 14]. Table 3a summarizes our contrastive pre-training settings on MedMNIST, following [15]. Table 3a shows the corresponding pre-training settings on CIFAR-10-LT, following the official MoCo demo on CIFAR-10 [14]. The contrastive learning model is pre-trained on 2 NVIDIA RTX3090 GPUs with 24GB memory each. The total number of model parameters is 55.93 million, among which 27.97 million requires gradient backpropagation.

Dataset Augmentation. We apply the same augmentation as in MoCo v2 [15] on all the images of RGB modalities to reproduce the optimal augmentation pipeline proposed by the authors, including PathMNIST, BloodMNIST, CIFAR-10-LT. Because OrganMNIST is a grey scale CT image dataset, we apply the augmentation in [3] designed for radiological images, replacing random gray scale and Gaussian blur with random rotation. Table 4 shows the details of data augmentation.

Repeated Augmentation. Our MoCo v2 pre-training is so fast in computation that data loading becomes a new bottleneck that dominates running time in our setup. We perform repeated augmentation on MedMNIST datasets at the level of dataset, also to enlarge augmentation space and improve generalization. [21] proposed repeated augmentation in a growing batch mode to improve generalization and convergence speed by reducing variances. This approach provokes a challenge in computing resources. Recent works [21, 50, 7] proved that fixed batch mode also boosts generalization and optimization by increasing mutiplicity of augmentations as well as parameter updates and decreasing the number of unique samples per batch, which holds the batch size fixed. Because the original contrastive learning works [13, 15] were implemented on ImageNet dataset, we attempt to simulate the quantity of ImageNet per epoch to achieve optimal performances. The details are shown in Table 5.

We only applied repeated augmentation on MedMNIST, but not CIFAR-10-LT. This is because we follow all the settings of the official CIFAR-10 demo [14] in which repeated augmentation is not employed.

## Turn 2 — document page 15 (rank 2 of 20)

Table 6: Benchmark settings. We apply the same settings for training MedMNIST, CIFAR-10, and CIFAR-10-LT.
| config | value |
|---|---|
| backbone | Inception-ResNet-v2 |
| optimizer | SGD |
| learning rate | 0.1 |
| learning rate schedule | reduce learning rate on plateau, factor=0.5, patience=8 |
| early stopping patience | 50 |
| max epochs | 10000 |
| augmentation | flip, p=0.5; rotation, p=0.5, in 90, 180, or 270 degrees; reverse color, p=0.1; fade color, p=0.1, 80% random noises + 20% original image |
| batch size | 128 |

## Turn 3 — document page 20 (rank 3 of 20)

This page contains only figures (Figure 9) and their caption discussing active querying strategies on CIFAR-10 and CIFAR-10-LT, including AUC scores for various strategies (BALD, Consistency, Coreset, Margin, VAAL, Entropy). There is no mention of optimizers or any training settings.

## Turn 4 — document page 6 (rank 4 of 20)

This page discusses querying strategies and their performance on medical imaging datasets. It mentions that for contrastive learning, they trained 200 epochs with MoCo v2, following its default hyperparameter settings. It also states that they applied repeated augmentation to reproduce large batch sizes and iteration numbers. However, this page does not specify the optimizer used for the contrastive learning training. The optimizer is mentioned in previous pages (e.g., page 14) as SGD.

## Turn 5 — document page 8 (rank 5 of 20)

This page contains Figure 5 and its caption, which discuss the importance of selecting a superior initial query in active learning. The caption mentions that hard-to-contrast data outperforms other initial queries and that the performance of the initial cycle (20 images) and the last cycle (50 images) are strongly correlated. The text also mentions that when fine-tuning from MoCo v2, the Pearson correlation coefficient between AUC20 and AUC50 remains high for various selection strategies. However, this page does not contain any information about the optimizers used in the research.

## Turn 6 — document page 4 (rank 6 of 20)

none
