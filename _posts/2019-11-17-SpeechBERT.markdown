---
layout:     post
title:     My Work - SpeechBERT：An Audio-and-text Jointly Learned Language Model for End-to-end Spoken Question Answering
author:     Jexus
tags: 		nlp speech_processing deep_learning
subtitle:   Interspeech 2020 conference paper
category:  project
---

# [SpeechBERT: An Audio-and-text Jointly Learned Language Model for End-to-end Spoken Question Answering](https://arxiv.org/abs/1910.11559)

> Updated in 2020/11/01 after published in Interspeech 2020

Authors: [**Yung-Sung Chuang (me)**](https://voidism.github.io/), [Chi-Liang Liu](https://github.com/Liangtaiwan), [Hung-Yi Lee](http://speech.ee.ntu.edu.tw/~tlkagk/index.html), and [Lin-shan Lee](http://speech.ee.ntu.edu.tw/previous_version/lslNew.htm)

ArXiv: [https://arxiv.org/abs/1910.11559](https://arxiv.org/abs/1910.11559)  

## Introduction

While various end-to-end models for spoken language understanding tasks have been explored recently, this paper is probably the first known attempt to challenge the very difficult task of end-to-end spoken question answering (SQA). Learning from the very successful BERT model for various text processing tasks, here we proposed an audio-and-text jointly learned SpeechBERT model. This model outperformed the conventional approach of cascading ASR with the following text question answering (TQA) model on datasets including ASR errors in answer spans, because the end-to-end model was shown to be able to extract information out of audio data before ASR produced errors. When ensembling the proposed end-to-end model with the cascade architecture, even better performance was achieved. In addition to the potential of end-to-end SQA, the SpeechBERT can also be considered for many other spoken language understanding tasks just as BERT for many text processing tasks.


## TL;DR in Chinese (for 1st version)

以往 Spoken Question Answering (SQA) 的 dataset 都需要先把語音用 ASR 語音辨識轉成文字之後，再當成一般的文字 QA dataset，接 QA model 下去做。然而前人指出，經過 ASR 後的文字因為包含辨識錯誤，會使得 SQA 的正確率與一般純文字 QA 相比大幅的降低 (甚至20%，如下圖)。

![](https://i.imgur.com/GgNWGxS.png)

因此我們做了大概是第一個 End-to-end 的 SQA 模型 - **SpeechBERT**。

![](https://i.imgur.com/zdwXgmz.png)

此模型藉助 pre-trained language model(BERT) 的方法，將語音跟文字用同一個 BERT (Cross-modal) model 下去做 pre-train，最後再 fine-tune 在 SQA 的 dataset 上，最後取得的 performance 已贏過過去 conventional 的 QA model，雖然跟 ASR + BERT 的方法還是差了一點，但在將 QA 題目以語音辨識的 Word Error Rate (WER) 分類後可以發現，在 WER 很高 (~80%) 的題目上 ASR + BERT 的方法會使錯題比例大幅提昇，而我們的 SpeechBERT 還是可以維持原有的水準。

![](https://i.imgur.com/VzQY8k4.png)