---
layout:     post
title:      Stanford - CS224n Natural Language Processing with Deep Learning - Course Notes
author:     Jexus
tags: 		NLP Machine_Learning Deep_Learning
subtitle:   CS224n (NLP with DL) 課程筆記
category:  note
---

>所有課程影片：https://www.youtube.com/playlist?list=PL3FW7Lu3i5Jsnh1rnUwq_TcylNr7EkRe

## Lecture 1 | Introduction to NLP and Deep Learning 
> [Slides](http://web.stanford.edu/class/cs224n/lectures/lecture1.pdf)  
> Suggested Readings:  
[Linear Algebra Review](http://web.stanford.edu/class/cs224n/readings/cs229-linalg.pdf)  
[Probability Review](http://web.stanford.edu/class/cs224n/readings/cs229-prob.pdf)  
[Convex Optimization Review](http://web.stanford.edu/class/cs224n/readings/cs229-cvxopt.pdf)  
[More Optimization (SGD) Review](http://cs231n.github.io/optimization-1/) 

第一堂課就是很top down方式的課程介紹，讓你大概了解整個NLP領域的Big picture。  
NLP著重在Syntactic analysis和Sementic Interpretation的部分。  
人類的語言是很奇怪的東西，他是discrete/symbolic/categorical的signal system。  
但科學家相信語言在人腦中encoding時是continuous pattern of activation，  
而語言傳播時也是透過continuous的信號，語言的sparsity對機器學習來說是個問題。  
2014年提出的word2vec也許是這個問題的解法，讓語言也能用continuous的方式在deep neural network中做optmization，下一堂課就會介紹word2vec。Deep learning在speech recognition和computer vision中，都已經有了突破性的進展，但NLP還是很爛。  

Applications:
- Sentiment Analysis -> 透過RecursiveNN
- Dialogue Agent -> 透過Recurrent Neural Network
- Machine Translation -> 透過wordvec + deep，目前做得最成功的NLP問題

最後來點平衡報導好了：https://medium.com/@culurciello/the-fall-of-rnn-lstm-2d1594c74ce0

## Lecture 2 | Word Vector Representations: word2vec
>[Slides](http://web.stanford.edu/class/cs224n/lectures/lecture2.pdf)  
>Suggested Readings:  
[Word2Vec Tutorial - The Skip-Gram Model](http://mccormickml.com/2016/04/19/word2vec-tutorial-the-skip-gram-model/)  
[Distributed Representations of Words and Phrases and their Compositionality](http://papers.nips.cc/paper/5021-distributed-representations-of-words-and-phrases-and-their-compositionality.pdf)  
[Efficient Estimation of Word Representations in Vector Space](http://arxiv.org/pdf/1301.3781.pdf)  

待補...
