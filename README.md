# SRCNN-pytorch

작성일시: 2020년 9월 14일 오후 3:41
주제: Super-Resolution
최종 편집일시: 2020년 9월 15일 오후 5:46

# Overview

## ECCV_2014

Super-Resolution

## Abstract

- Single Image Super-Resolution (SISR)에 Deep Learning 방법을 적용하였다.
- End-to-end로 CNN Network를 학습하여 저해상도 영상을 고해상도로 영상으로 변환해준다.
- 성능과 속도 사이의 trade-off를 위해 여러 network구조와 parameter를 실험하였다.
- 3 color channels를 동시에 다루고, 전체적으로 좋은 성능을 보임을 보여준다.

# Introduction

- SISR 문제는 ill-posed 문제로서 유일한 정답이 존재하지 않는 문제이다.
    - example based strategy와 같은 강력한 prior information에 의해 solution space를 고정하여 문제를 해결해왔다.
    - example based strategy : 동일한 이미지의 내부 유사성을 이용하거나, external low-resolution 과 high-resolution 쌍을 이용하여 매핑하는 기술을 학습하는 전략
- Dictionaries나 manifolds를 학습해야하는 기존의 방법들과 다르게 CNN을 이용하여 low-resolution과 high-resolution을 end-to-end로 학습한다.
- Contributions
    1. SISR을 위한 end-to-end CNN을 제안하였다.
    2. deep learning based SR method를 전통적인 super-resolution 관점에서 해석하여 각각의 layer가 patch extraction, nonlinear mapping, reconstruction을 담당한다고 서술한다.
    3. deep learning based SR method가 super resolution 분야에서도 적용이 가능함을 보였다.

 

# Method

<img width="719" alt="_2020-09-14__7 58 51" src="https://user-images.githubusercontent.com/33571876/93203622-b22e8a80-f78f-11ea-8cb1-6fd7f0d764c8.png">

SRCNN은 먼저 bicubic interpolation을 사용하여 low-resolution image를 목표하는 size로 upscaling 해준다. 이후 이렇게 upscaling된 low-resolution image를 high-resolution image로 만들어주기 위해서 1)Patch extraction and representation, 2)Non-linear mapping, 3)Reconstruction의 과정을 거치게 된다.

## Patch extraction and representation

- low-resolution image에서 patch들을 추출하고 이 patch들을 고차원 벡터로 표현한다.

## Non-linear mapping

- 위에서 구한 고차원 벡터를 non-linear함수를 통해 다른 고차원 벡터로 나타낸다. (high-resolution patch representation)

## Reconstruction

- high-resolution patch representation을 종합하여 최종 high-resolution image를 생성하게되고, 이 image는 ground truth와 유사하게 생성되어야한다.

위의 과정들은 $F(Y)=max(0,W*Y+B)$ 이런 수식을 거치게 되고, 이는 convolution layer를 거친 후 relu를 취해준것과 같다. Network자체로는 간단한 CNN구조를 사용하였지만, 각각의 layer를 전통적인 super-resolution관점으로 해석하였다.

## Training

- MSE loss를 사용하였고, evaluation matrices으로 PSNR, SSIM, MSSIM등 다양한 지표로 성능을 관찰하였다.
- 경험적으로 마지막 layer에서 더 작은 learning rate를 줬을 때 network의 수렴에 도움이 되어 앞의 두 layer는 $10^{-4}$, 마지막 layer는 $10^{-5}$로  할당하였다.

# Experiments

network의 성능에 깊이나 filter의 크기,수 등의 요인들이 어떻게 작용하는지를 확인하기 위해 여러 실험을 하였다. 초창기의 연구이기 때문에 특별한 사항이 없어 이 부분은 넘어가도록 한다.  

# Code

[yt-oh96/SRCNN-pytorch](https://github.com/yt-oh96/SRCNN-pytorch)

# References

[Single Image Super Resolution using Deep Learning Overview](https://hoya012.github.io/blog/SIngle-Image-Super-Resolution-Overview/)

[Image Super-Resolution Using Deep Convolutional Networks](https://arxiv.org/abs/1501.00092)

[yjn870/SRCNN-pytorch](https://github.com/yjn870/SRCNN-pytorch)

[Deep Learning for Super-Resolution: A Survey (1)](http://jaejunyoo.blogspot.com/2019/05/deep-learning-for-SISR-survey-1.html)

# Follow-up Tasks

ShCNN (NIPS_2015)

[https://papers.nips.cc/paper/5774-shepard-convolutional-neural-networks](https://papers.nips.cc/paper/5774-shepard-convolutional-neural-networks)
