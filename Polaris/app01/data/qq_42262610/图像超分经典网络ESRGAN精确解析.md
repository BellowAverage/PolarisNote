
--- 
title:  图像超分经典网络ESRGAN精确解析 
tags: []
categories: [] 

---
**改进**

<img alt="" height="273" src="https://img-blog.csdnimg.cn/c24e5099a5da429f8bdd814151b7fb4c.png" width="894">

**为了进一步提高SRGAN的恢复图像质量，我们主要对发生器G的结构做了两个修改:1)去除所有BN层;2)用所提出的残差中残密块(residual -in- residual密块，RRDB)代替原来的基本块，它结合了多级残差网络和密集连接。**

**在不同的psnr导向任务(包括SR和去模糊)中，去除BN层已被证明可以提高性能并降低计算复杂度。BN层在训练过程中使用批量的均值和方差对特征进行归一化，在测试过程中使用整个训练数据集的估计均值和方差。当训练数据集和测试数据集的统计差异较大时，BN层容易引入不愉快的工件，限制泛化能力。**

**除了改进的架构，我们还利用了一些技术来促进训练一个非常深入的网络:1)残差缩放[21,20]，即在将残差添加到主路径之前，通过在0到1之间乘一个常数来缩小残差，以防止不稳定;2)更小的初始化，因为我们的经验发现，当初始参数方差变小时，残差架构更容易训练。**

**除了改进了发生器的结构外，我们还改进了基于相对论GAN[2]的鉴别器。与标准鉴别器Din SRGAN估计一个输入图像x是真实和自然的概率不同，相对论鉴别器试图预测真实图像xr相对于假图像xf更真实的概率。**

**我们还开发了一种更有效的感知损失lperception，通过在激活前约束特征，而不是像SRGAN中那样在激活后约束特征。**

**感知损失在预先训练的深度网络的激活层上预先定义，其中两个激活特征之间的距离是最小的，与惯例相反，我们建议在激活层之前使用特性，这将克服原始设计的两个缺点。首先，激活的特征是非常稀疏的，特别是在一个非常深的网络之后，例如，图像“狒狒”在VGG19-543层后激活神经元的平均百分比仅为11.17%。稀疏激活提供了薄弱的监督，从而导致较差的性能。其次，使用激活后的特征也会导致重建亮度与地面真实图像不一致。**

**我们已经提出了一个ESRGAN模型，它比以前的SR方法获得了一致更好的感知质量。该方法在感知指标方面获得了PIRM-SR挑战赛的第一名。我们制定了一个包含多个RRDB块的新架构，没有BN层。此外，利用残差缩放和更小的初始化等有用的技术来促进所提出的深度模型的训练。我们还介绍了使用相对论GAN作为鉴别器，它学会判断一个图像是否比另一个图像更真实，引导生成器恢复更详细的纹理。此外，我们利用激活前的特征增强了感知损失，提供了更强的监督，从而恢复更准确的亮度和逼真的纹理。**
