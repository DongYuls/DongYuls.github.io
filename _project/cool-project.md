---
layout: project_single
title:  "Residual Error based Anomaly Detection using Auto-Encoder in SMD Machine"
slug: "cool-project"
---

## Abstract

Suppressing bones on chest X-rays such as ribs and clavicle is often expected to improve pathologies classification. These bones can interfere with a broad range of diagnostic tasks on pulmonary disease except for musculoskeletal system. Current conventional method for acquisition of bone suppressed X-rays is dual energy imaging, which captures two radiographs at a very short interval with different energy levels; however, the patient is exposed to radiation twice and the artifacts arise due
to heartbeats between two shots. In this paper, we introduce a deep generative model trained to predict bone suppressed images on single energy chest X-rays, analyzing a finite set of previously acquired dual energy chest X-rays. Since the relatively small amount of data is available, such approach relies on the methodology maximizing the data utilization. Here we integrate the following two approaches. First, we use a conditional generative adversarial network that complements the traditional regression method minimizing the pairwise image difference. Second, we use Haar 2D wavelet decomposition to offer a perceptual guideline in frequency details to allow the model to converge quickly and efficiently. As a result, we achieve state-of-the-art performance on bone suppression as compared to the existing approaches with dual energy chest X-rays.


## Code 

This is the implementation of the paper "Residual Error based Anomaly Detection Using Auto-Encoder in SMD Machine Sound" by Dong Yul Oh and Il Dong Yun.

For more information check out the paper [PDF] on MDPI Sensors.

All of these scripts are based on the [sample] dataset provided in our paper. Note that all rights reserved to [Crevis Co., Ltd], and only a few samples for the SMD machine sound can be released. The experimental results of this demo may differ (have poorer performance) from those in the paper because of the lack of training data.
