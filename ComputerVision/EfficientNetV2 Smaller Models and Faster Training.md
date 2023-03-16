# EfficientNetV2: Smaller Models and Faster Training

## MetaData

Submitted on 1 Apr 2021 (v1), last revised 23 Jun 2021 (this version, v3)

### URL

[Github](https://github.com/google/automl/tree/master/efficientnetv2) |
[arXiv](https://arxiv.org/abs/2104.00298) | [Colab](https://colab.research.google.com/github/google/automl/blob/master/efficientnetv2/tfhub.ipynb) | [TF-Hub](https://tfhub.dev/google/collections/efficientnet_v2/1)

### Domain

Computer Vision-Image Classification

### Keywords

Image Classification, Deep Neural Networks, Parameter Efficiency

### Cite

[Bibtex](@tan2021efficientnetv2)

## Details

### Research Question

- Can we further improve training speed and parameter efficiency?

### Study on EfficientNetV1

1. Training with very large image sizes is slow and using smaller image size for training also leads to better accuracy
2. Depth Wise Convolutions are slow (as they cannot utilize modern accelerators) in early layers but effective in later stages
3. Equally scaling up every stage is sub-optimal. In addition, EfficientNet's aggressively scale up image size, leading to large memory consumption and slower training.

### Contribution

1. Introduced EfficientNetV2, a new family of smaller and faster models found using training-aware NAS
2. Improved methods of Progressive Learning which in result speeds up training and improves training accuracy
3. Demonstrated up-to 11x faster training speed and up-to 6.8x faster better parameter efficiency.

### Method

1. EfficientNetV2 Architecture Design

> -	As Depth Wise Convolutions are slow in early layers, Fused-MBConv is used to better utilize mobile server or server accelerators.
-	Best Combination of Fused-MBConv and MBConv is done using neural architecture search.
> 
> 
> ![architecture.jpg](EfficientNetV2%20Smaller%20Models%20and%20Faster%20Training%202a48e715836c4960a1993970ece1d55b/architecture.jpg)
> 
1. Training Aware NAS and Scaling
    
    > Aims to jointly optimize accuracy, parameter efficiency and training efficiency on modern accelerators.
    > 
    
    > Search Space is a stage-based factorized space with design choices for various hyperparameters
    > 
    
    > Different stages are scaled at different rates(more layers are added to later stages) and maximum image size is limited to 480 to reduce training speed overhead.
    > 
2. Progressive Learning with Adaptive Regularization
    - Image sizes are dynamically changed during training. As a result, regularization has also to be adjusted adaptively along with image size during training
        
        ![progressive-resize.png](EfficientNetV2%20Smaller%20Models%20and%20Faster%20Training%202a48e715836c4960a1993970ece1d55b/progressive-resize.png)
        
    - Types of regularization adjusted adaptively are:
    
    > 1. Dropout
     2. RandAugment-An automated Augmentation Tool
     3. Mixup
    > 
    
    ![adaptive-reg.png](EfficientNetV2%20Smaller%20Models%20and%20Faster%20Training%202a48e715836c4960a1993970ece1d55b/adaptive-reg.png)
    

### Dataset used

[CIFAR-10](https://paperswithcode.com/dataset/cifar-10)

[ImageNet](https://paperswithcode.com/dataset/imagenet)

[CIFAR-100](https://paperswithcode.com/dataset/cifar-100)

[Oxford 102 Flower](https://paperswithcode.com/dataset/oxford-102-flower)

[Stanford Cars](https://paperswithcode.com/dataset/stanford-cars)

### Results

1. By pretraining on the same ImageNet21k,EfficientNetV2 achieves 87.3% top-1 accuracy on ImageNet ILSVRC2012, outperforming the recent ViT by 2.0% accuracy while training 5x-11x faster using the same computing resources.EfficientNetV2-L(21k) improves the top-1 accuracy by 1.5% (85.3% vs 86.8%), using 2.5x fewer parameters and 3.6x fewer FLOPs, while running 6x - 7x faster in training and inference.
2. caling up data size is more effective than simply scaling up model size in high-accuracy regime when thetop-1 accuracy is beyond 85%, it is very difficult to further improve it by simply increasing model size due to overfitting

![res1](EfficientNetV2%20Smaller%20Models%20and%20Faster%20Training%202a48e715836c4960a1993970ece1d55b/result1.png)

res1

![res2](EfficientNetV2%20Smaller%20Models%20and%20Faster%20Training%202a48e715836c4960a1993970ece1d55b/result2.png)

res2

![res3](EfficientNetV2%20Smaller%20Models%20and%20Faster%20Training%202a48e715836c4960a1993970ece1d55b/result3.png)

res3

![res4](EfficientNetV2%20Smaller%20Models%20and%20Faster%20Training%202a48e715836c4960a1993970ece1d55b/result4.png)

res4

### Conclusion

- Proposed a new family of smaller
and faster neural networks for image recognition
