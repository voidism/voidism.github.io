---
layout:     post
title:      Which layer preserves the best cross-lingual representations in multilingual-BERT?
author:     Jexus
tags: 		NLP deep_learning
subtitle:   Small experiments on multilingual-BERT
category:  notes
---

# Which layer preserves the best cross-lingual representations in multilingual-BERT?

In the context of NLP research, variant in different languages is a non-negligible issue that does not appear in other DL research fields (e.g. Computer Vision). There are over 7000 languages in the world, while most of the NLP datasets/corpus are in English. Cross-lingual transfering from English to other languages is desirable especially for the languages with fewer training data.

Before BERT appeared, the main research about cross-lingual transfering focusing on aligning independent monolingual word embeddings for different languages in supervised/adversarial methods (e.g. [MUSE](https://arxiv.org/pdf/1710.04087.pdf)). However, after Google released the Multi-lingual version of BERT (Multilingual-BERT), people surprisingly found cross-lingual transferability in BERT for many languages without any supervision or adversarial training process ([How multilingual is Multilingual BERT?](http://arxiv.org/abs/1906.01502), [Zero-shot Reading Comprehension by Cross-lingual Transfer Learning with Multi-lingual Language Representation Model](https://arxiv.org/abs/1909.09587)). 

I found this interesting phenomenon last summer, and I did some t-SNE visualization on BERT hidden contextualized representations (from 8-th layer) using WMT-17 paired en-zh corpus.

![](https://i.imgur.com/geFX8rh.png)
> if you understand Chinese, it is a shock to see perfectly matching between the Chinese words with the English counterparts.

I also visualized each different layer in BERT, it seems that the most aligned layer is layer 7~8. On the contrary, the first few layers (1~4) and the last (11~12) are not aligned nicely.



![features from different layers](https://i.imgur.com/agcOuNx.gif)
> there are 12 pictures in this GIF from 12 different BERT layers.

To examine the alignment quality of BERT in different layers, I did some experiments on XNLI, a dataset to test the cross-lingual transferability of NLI models. To be fairly compared, I did not extract the features directly from each layer to feed into a XNLI model, because different layers have different level of functions to natural language understanding task, and lower level features may not get good enough results on XNLI even if they are aligned correctly.

Instead, I fixed the first N layers of BERT model and train the layers after N on XNLI dataset (so the whole model size that data propagate through is maintained). 

![](https://i.imgur.com/AQPj7Wd.png)
> experimental results of XNLI

The results show that performance on XNLI directly correlated with the visualized alignment quality of BERT. The the representation from layer 8 is better for cross-lingual transfer. On the other hand, the performance of English dataset is not significantly affected by the layer number we fixed. 

![](https://i.imgur.com/jX8ti9d.png)
> visualization of XNLI results
> -1 means finetune all  
> 0 means finetune except embedding layer  
> 1~11 means the first N-th layer is fixed