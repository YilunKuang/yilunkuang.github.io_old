---
layout: archive
title: ""
permalink: /resource/large_scale_ml_training
author_profile: true
---

# Large-Scale Machine Learning Training

## Introduction

This is a list of resources for the engineering aspect of machine learning, especially self-supervised training of deep neural networks on multi-node machines. 

## Distributed Training

### PyTorch DDP

To quickly implement distributed training on PyTorch, I recommend this tutorial from Princeton University.

+ (Tutorial) [Tutorial on PyTorch Distributed Data Parallel (DDP)](https://github.com/PrincetonUniversity/multi_gpu_training/tree/main/02_pytorch_ddp)


### Parallel Computing

To know more about design principles of parallel hardware and software, MPI on distributed-memory systems, OpenMP/Pthreads on shared-memory systems, and CUDA programming on GPUs, Peter Pacheco and Matthew Malensek's textbook is a good way to start. 

+ (Book) [An Introduction to Parallel Programming](https://www.cs.usfca.edu/~peter/ipp2/index.html)

### SLURM

SLURM is a typical job management system on HPC clusters. 

+ (Documentation) [SLURM Cheat Sheet](https://slurm.schedmd.com/pdfs/summary.pdf)

## Hyperparameter Tuning

### Learning Rate

Learning rate tuning for SGD methods is sometimes inevitable step for publications in applied ML literatures. Here is a list of resources for how to do this correctly:

+ (Blog) [A Recipe for Training Neural Networks - Andrej Karpathy blog](http://karpathy.github.io/2019/04/25/recipe/)
+ (Paper) [SGD Tricks](https://leon.bottou.org/publications/pdf/tricks-2012.pdf)

Layer-wise Adaptative Rate Scaling (LARS) helps with large multi-node systems with huge effective batch size.

+ (Paper) [LARS](https://arxiv.org/abs/1708.03888)

## Improving ML Efficiency

### MosaicML

MosaicML is a start-up for building efficient ML systems. MosaicML Composer is an open-source library for ML training/inference speedup, cost reduction, resource reduction based on algorithmic methods. 

+ (Website) [MosaicML](https://www.mosaicml.com/)
+ (Documentation) [MosaicML Composer](https://docs.mosaicml.com/)

### FFCV

FFCV is a tool for faster dataloading. 

+ (Tool) [FFCV](https://ffcv.io/)

### Albumentations

Albumentations supports faster data augmentations in computer vision applications. 

+ (Tool) [Albumentations](https://albumentations.ai/)

### Mixed Precision Training

Mixed Precision Training incorporate float16 to the ML training pipeline for reduced memory usage and faster arithmetic.

+ (Paper) [Mixed Precision Training](https://arxiv.org/pdf/1710.03740.pdf)

### Lottery Ticket Hypothesis

Lottery Ticket Hypothesis claims the existence of a subnetwork from a neural networks that can achieve comparable inference accuracy compared to the original network. 

+ (Paper) [The Lottery Ticket Hypothesis: Finding Sparse, Trainable Neural Networks](https://arxiv.org/pdf/1803.03635.pdf)

## Performance Monitoring

### Command Line Functionality

Linux Time Command is a great way to track the user time and system time in your machine. 

+ (Documentation) [Time](https://man7.org/linux/man-pages/man1/time.1.html)

Nvidia Nsight is a kernel profiling tool for extracting FLOP performance. 

+ (Tool) [NVIDIA Nsight Compute](https://developer.nvidia.com/nsight-compute)

The easiest command for checking GPU memory usage is 

+ (Command) `nvidia-smi`

### NVIDIA Deep Learning Performance Guide

For monitoring deep learning performance on NVIDIA GPUs, here is a way to start.

+ (Documentation) [NVIDIA Deep Learning Performance Guide](https://docs.nvidia.com/deeplearning/performance/index.html)

### Roofline Modeling

Roofline Model is a visualization of the compute / memory bottleneck of the current running program.

+ (Paper) [Roofline: An Insightful Visual Performance Model for Floating-Point Programs and Multicore Architectures](https://people.eecs.berkeley.edu/~kubitron/cs252/handouts/papers/RooflineVyNoYellow.pdf)

### Torch Profiler

To have an in-depth examination of which operations cause the performance bottleneck, torch profiler provides a detailed stack traces and performance metrics

+ (Tool) [Torch Profiler](https://pytorch.org/docs/stable/profiler.html)

### TensorBoard

TensorBoard allows you to visualize metrics during your ML training. TensorBoard is also compatible with PyTorch Profiler. 

+ (Tutorial) [TensorBoard](https://www.tensorflow.org/tensorboard)
+ (Tutorial) [PyTorch Profiler with TensorBoard](https://pytorch.org/tutorials/intermediate/tensorboard_profiler_tutorial.html)

### Weights and Biases

Weights and Biases (wandb) is a great MLOps platform for general machine learning engineering purposes

+ (Tool) [Weights & Biases](https://wandb.ai/site)

### TorchSummary

TorchSummary is a package for getting model memory usage

+ (Tool) [torch-summary 1.4.5](https://pypi.org/project/torch-summary/)

## Deployment

### Containers

Docker and Singularity are two commonly used containers for shipping ML products. I recommend the Docker playlist from the youtuber “TechWorld with Nana” for a quick start on learning about basic concepts in Docker.

+ (Video) [TechWorld with Nana - Playlist](https://www.youtube.com/c/TechWorldwithNana/playlists)
+ (Tutorial) [Introduction to Singularity](https://docs.sylabs.io/guides/3.5/user-guide/introduction.html)

### Kubernetes

Kubernetes is a tool for orchestrating multiple containers. Typically in a machine learning workflow, there could be multiple containers for inference, online-training, storage etc. I recommend the Kubernetes playlist from the youtuber TechWorld with Nana for a quick start on learning about basic concepts in Kubernetes

+ (Video) [TechWorld with Nana - Playlist](https://www.youtube.com/c/TechWorldwithNana/playlists)

## Other Resources

Here is a miscellaneous collection of resources

+ (Blog) [How to Train Really Large Models on Many GPUs?](https://lilianweng.github.io/posts/2021-09-25-train-large/)
+ (Tutorial) [Rules of Machine Learning: Best Practices for ML Engineering](https://martin.zinkevich.org/rules_of_ml/rules_of_ml.pdf)
+ (Tutorial) [How to be an effective Deep Learning Researcher/Engineer (MIT Deep Learning)](https://www.dropbox.com/s/3iv93falplmt0yc/8_effective_dl.pdf?dl=0)
+ (Slide) [DIY Deep Learning: Advice on Weaving Nets](http://6.869.csail.mit.edu/fa19/lectures/DIY_Deep_Learning_MIT_6.869.pdf)

