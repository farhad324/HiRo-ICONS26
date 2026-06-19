# \[🧠ICONS 2026\] HiRo: A Compact Four-Directional Hierarchical Reservoir Token-Mixer for Efficient Image Classification


- *HiRo: A Compact Four-Directional Hierarchical Reservoir Token-Mixer for Efficient Image Classification*  
- Accepted at **ACM International Conference on Neuromorphic Systems (ICONS) 2026** 
- **arXiv Preprint:** [arXiv:2606.15151](https://arxiv.org/abs/2606.15151) <br />
- **Authors:** Md Farhadul Islam, Ishan Thakkar & J. Todd Hastings


## Overview

In this work, we propose HiRo, a parameter-efficient image classification framework that combines shifted-window partitioning with multi-directional hierarchical reservoir computing. Images are represented as patch tokens and processed within local windows using four directional scans. Each directional sequence is passed through a two-stage slice-and-mix reservoir module, where fixed recurrent reservoirs provide nonlinear token mixing while only lightweight readouts are trained.

By alternating regular and shifted windows, HiRo supports both local spatial modeling and low-cost cross-window interaction. This allows the model to achieve efficient visual representation learning with under 1M trainable parameters, while remaining closely connected to the broader goals of physical reservoir computing.


## Architecture

**Architecture Summary**:

- Input image is divided into non-overlapping patches.
- Each patch is linearly projected and normalized.
- Fixed **2D sinusoidal positional encoding** is added.
- Tokens are processed by stacked **WHR blocks**:
  - Block 1: Regular window partitioning
  - Block 2: Shifted window partitioning
- Inside each window:
  - Tokens are scanned in four directions.
  - Each directional sequence is split into equal slices.
  - Stage-1 fixed reservoirs process token-level slices.
  - Start, end, and mean slice features are summarized.
  - Stage-2 fixed reservoirs mix slice summaries.
  - Mixed slice outputs are expanded back to token level.
  - Four directional outputs are realigned and averaged.
- Final token features are globally averaged.
- A lightweight two-layer MLP head produces class logits.


## Benchmark Results

| Dataset | Accuracy | Precision | Recall | F1 |
|--------|----------|-----------|--------|----|
| **MNIST** | **99.46** | **99.47** | **99.45** | **99.46** |
| **CIFAR-10** | **85.57** | **85.60** | **85.57** | **85.58** |
| **CIFAR-100** | **59.10** | **59.34** | **59.10** | **59.03** |

> 🧪 HiRo achieves competitive accuracy while using fewer than 1M trainable parameters, outperforming ViT and Swin on CIFAR-10 and CIFAR-100 in the reported experiments.


## Efficiency

| Dataset | Trainable Params | Epoch Time | Inference Time | Peak Train Memory | Peak Inference Memory |
|--------|------------------|------------|----------------|-------------------|-----------------------|
| **MNIST** | **0.887M** | **31.84s** | **3.06s** | **692.7 MB** | **171.1 MB** |
| **CIFAR-10** | **0.887M** | **39.40s** | **3.53s** | **1120.7 MB** | **224.2 MB** |
| **CIFAR-100** | **0.898M** | **40.84s** | **3.54s** | **1118.8 MB** | **223.7 MB** |


