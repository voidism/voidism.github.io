---
layout:     post
title:     My Work - SpeechBERT：Cross-Modal Pre-trained Language Model for End-to-end Spoken Question Answering
author:     Jexus
tags: 		EMNLP nlp speech_processing deep_learning
subtitle:   Submitted to ICASSP 2020 (International Conference on Acoustics, Speech and Signal Processing)
category:  project
---

# [SpeechBERT: Cross-Modal Pre-trained Language Model for End-to-end Spoken Question Answering](https://arxiv.org/abs/1910.11559)

_Submitted to ICASSP 2020 (International Conference on Acoustics, Speech and Signal Processing)_

Authors: [**Yung-Sung Chuang**](https://voidism.github.io/), [Chi-Liang Liu](https://github.com/Liangtaiwan), and [Hung-Yi Lee](http://speech.ee.ntu.edu.tw/~tlkagk/index.html)

ArXiv: [https://arxiv.org/abs/1910.11559](https://arxiv.org/abs/1910.11559)  

## Introduction

While end-to-end models for spoken language understanding tasks have been explored recently, there is still no end-to-end model for spoken question answering (SQA) tasks, which would be catastrophically influenced by speech recognition errors. Meanwhile, pre-trained language models, such as BERT, have performed successfully in text question answering. To bring this advantage of pre-trained language models into spoken question answering, we propose SpeechBERT, a cross-modal transformer-based pre-trained language model. As the first exploration in end-to-end SQA models, our results matched the performance of conventional approaches that fed with output text from ASR and only slightly fell behind pre-trained language models, showing the potential of end-to-end SQA models.


## Summary in Chinese

以往 Spoken Question Answering (SQA) 的 dataset 都需要先把語音用 ASR 語音辨識轉成文字之後，再當成一般的文字 QA dataset，接 QA model 下去做。然而前人指出，經過 ASR 後的文字因為包含辨識錯誤，會使得 SQA 的正確率與一般純文字 QA 相比大幅的降低 (甚至20%，如下圖)。

![](https://i.imgur.com/GgNWGxS.png)

因此我們做了大概是第一個 End-to-end 的 SQA 模型 - **SpeechBERT**。

![](https://i.imgur.com/zdwXgmz.png)

此模型藉助 pre-trained language model(BERT) 的方法，將語音跟文字用同一個 BERT (Cross-modal) model 下去做 pre-train，最後再 fine-tune 在 SQA 的 dataset 上，最後取得的 performance 已贏過過去 conventional 的 QA model，雖然跟 ASR + BERT 的方法還是差了一點，但在將 QA 題目以語音辨識的 Word Error Rate (WER) 分類後可以發現，在 WER 很高 (~80%) 的題目上 ASR + BERT 的方法會使錯題比例大幅提昇，而我們的 SpeechBERT 還是可以維持原有的水準。

![](https://i.imgur.com/VzQY8k4.png)