---
layout:     post
title:      Speech Notes - Hardware-Centric AutoML, Design Automation for Efficient Deep Learning Computing
author:     Jexus
tags: 		Speech AutoML NAS
subtitle:   2019/01/09 Song Han 教授演講速記
category:  note
---


# Hardware-Centric AutoML: Design Automation for Efficient Deep Learning Computing

- Prof. [Song Han, Massachusetts Institute of Technology (MIT)](https://songhan.mit.edu/)
- 2019-01-09 2:00pm-3:00pm

![](https://i.imgur.com/53Jx9bH.png)

這筆記很早已前就做了（今天是2019/12/03），現在才想到要放。當天演講很深刻的一點是，講者想要表達，過去我們做電路 IC design，只要寫 RTL code 定義好功能，接下來使用 EDA tools 來優化就好，這樣的分工體系十分有效率。這樣的流程，未來將重現在 Deep Learning 領域，到時候可能只需要定義好 Network 功能大架構及 training data，剩下的交給 AutoML、NAS 生出 network，並且再透過pruning、quantization等優化到晶片上，又小又快，不用再透過大量人工調參達成目的。

## 前言

- ImageNet become MNIST
- moore's law 放緩

## 實驗室在做啥
- video understanding 
- 3d recognition
- architecture search
- deep compression
- sparsity
- multi-precise

## 當前work
### Pruning(NIPS'15)
- PhD時期就開始做的
- 有生物學基礎，如人嬰幼兒時期也會大量pruning自己的神經元
- pruning到一個程度之後，準確率會下降，不過沒關係，維持該架構重新再train，準確率回復到原本，就這樣持續做幾個iteration，甚至可以刪到剩下90%而準確率幾乎沒有下降，CNN可以，RNN LSTM也可以(一開始訓練，network的冗餘是必要的)
- 這個東西已經上市了=>在DNNDK裡面(DEEPHi)
- 對於Object detection task 可以提供 5.7倍的speed up

### Trained quantization(ICLR'16) 最小4bit就夠了~
- 從32bit減到8bit，最基本方法是小的權重就刪掉
- Pruning + Quantization 這兩步驟成為標準pipeline => 開公司了~[深鑒科技](http://www.deephi.com/)
- 在pruning完之後，再做稀疏化處理矩陣，做儲存所需空間更小，可以稀疏到90%
- 做馬路上的object detection，要做成real time，還沒壓縮，只能16FPS，很卡，壓縮了90%之後，可以125FPS，超強的。

### **A**utoML for **M**odel **C**ompression (AMC)

- 太多公司都在做硬體上面放DNN，因此一堆人都需要一樣的技術，害他們公司很忙，如果每個model都需要人來做Pruning + Quantization實在是太累太花人力了。於是他們就想到，人們以前做IC design的時候也是看layout畫得很累，於是想要自動化，就跑出EDA這個領域，現在做Deep Learning壓縮好像遇到一樣的問題，也是可以如法炮製，做一個**Hardware-aware AutoML**

- 用RL學習自動決定如何刪除冗餘的網路，reward是錯誤率，想不到跟手動調參壓縮比起來會完勝，而且只花了四個小時，準確率更高了，計算量跟accuracy都上升了。

- AMC之後發現，3x3的kernel被砍最嚴重，1x1的kernel被砍最少，這是人在手動調參壓縮Model時沒有觀察到的。在object detection的model上可以壓得非常多。

- sumsung手機使用了此技術，雖然沒有提供sparsity稀疏化矩陣運算，但是直接砍掉一些channel也達成很好的效能提升而不失正確率。

### ProxylessNAS

- 能不能直接設計高效率的model，為不同的硬體直接設計她們適合的model架構呢? GPU跟CPU跟手機晶片適合的架構一定不一樣，於是就有了NAS(neural architecture search)
- 一樣用RL的方法，硬體延遲latency透過公式建模也是可以微分的，就直接當成reward，把硬體的耗能也當成reward，硬train一發，最後發現estimate的latency跟實際的latency幾乎一樣，而結果準確率上升，latency下降，比人類自己設計的還好。

### 自動化Quantization(HAQ)
- 其實蘋果發布會上晶片就有號稱multiprecistion support，也就是支援各種浮點數運算
- 用actor-critic的方法做，發現機器學習到pointwise need less bits，depthwise need more bits

### From 2D conv to 3D conv
- temporal modeling ，也就是判斷video的連續動作及預測，需要用3D CNN來做才行，但是運算量爆幹大，於是作出TSM video model，讓他可以用2D conv的運算量實現3D conv。throughput 變很短。

### AI assisted CAD tools
- 尤其是類比電路，因為不像數位電路有EDA，沒有自動化工具，特別需要

- 設計電路參數，現在用seq2seq做，讀了一個電路，輸出個個電晶體所需的W(channel width)、L(channel length)、R(resistor)、C(capacitor)，不再需要人來設計電路，而是由機器來調參，這次是電路的參數，以後就不用靠人IC design惹。

- Design automation for neural networks

![](https://i.imgur.com/IUZ0oBt.png)
