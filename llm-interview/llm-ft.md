


## 微调




> 介绍下 LoRA、AdaLoRA、QLoRA 这几种高效微调方法及其特点

  
> 在LoRA中，A和B低秩矩阵的初始化方法，对A采用高斯初始化，对B采用零矩阵初始化，目的是让训练刚开始时BA的值为0，这样不会给模型带来额外的噪声。那么，对A做零矩阵初始化，对B做高斯初始化行不行呢？反正看起来只要让初始化为0就行？

当前作者还没有发现转换初始化方式产生的显著区别，只要这两者中任意一者为0，另一者不为0即可。

参考：https://github.com/microsoft/LoRA/issues/98





> 介绍下 Prefix Tuning、Prompt Tuning、P-Tuning、P-Tuning v2 这四种高效微调方法的区别与联系？

1. Prompt Tuning和P-Tuning都是只在Embbedding层加入虚拟Token。而 Prefix Tuning、P-Tuning v2 会在每一层都加入虚拟Token，从而引入了更多的可训练参数；通过加入到更深层结构中的Prompt，能给模型预测带来更直接的影响。
2. P-Tuning通过 LSTM + MLP 去编码这些virtual token，再输入到模型，可以让模型收敛更快。
3. Prefix Tuning 为了防止直接更新 Prefix 的参数（virtual token）导致训练不稳定和性能下降的情况，在Prefix层前面加了MLP结构，训练完成后，只保留Prefix的参数。





