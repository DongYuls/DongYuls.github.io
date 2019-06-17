---
layout: project_single
title: "Longitudinal Change Detection on Chest X-rays using Geometric Correlation Maps"
slug: "change-detection"
---

## Abstract

The diagnostic decision for chest X-ray image generally considers a probable change in a lesion, compared to the previous examination. We propose a novel algorithm to detect the change in longitudinal
chest X-ray images. We extract feature maps from a pair of input images through two streams of convolutional neural networks. Next we generate the geometric correlation map computing matching scores for every possible match of local descriptors in two feature maps. This correlation map is fed into a binary classifier to detect specific patterns of the map representing the change in the lesion. Since no public dataset offers proper information to train the proposed network, we also build our own dataset by analyzing reports in examinations at a tertiary hospital. Experimental results show our approach outperforms previous methods in quantitative comparison. We also provide various case examples visualizing the effect of the proposed geometric correlation map.

## Note

This work has been accepted for Medical Image Computing and Computer Assisted Intervention (MICCAI) 2019. For more information, the original paper [PDF]() will be available shortly on MICCAI 2019 Proceedings.
