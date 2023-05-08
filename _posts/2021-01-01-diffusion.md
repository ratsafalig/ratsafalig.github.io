---
title: Diffusion 模型
tag:
- AI
- Diffusion
categories:
- AI
- Diffusion
---

Diffusion Model（扩散模型）是一种生成模型，用于对高维数据分布进行建模。它最初是由Tieleman和Hinton提出的，其目的是解决一些传统机器学习技术在处理大规模高维数据方面效果不佳的问题。Diffusion Model的核心思想是通过迭代 diffusing（扩散）噪声分布来逐渐逼近目标数据分布。

Diffusion Model的一个重要组成部分是Diffusion Process。它从噪声分布开始，每次应用一系列可逆转换（如双向LSTM），每一步都会将噪声“扩散”一段距离到达“目标分布”。最终，Diffusion Process通过多次迭代之后，得到了一个可以近似地表示目标数据分布的随机变量。

Diffusion Model主要用于生成高维连续数据，这包括生成图像、音频等数据类型。它具有很强的模型表达能力和生成能力，被广泛应用于计算机视觉、自然语言处理等领域。

# 傻瓜原理

抓一个 diffusion 模型的代码实现来说一说 diffusion 模型的实现。代码完整详见 [Link](#link)  

给定一个 (x, y) 的图像，生成一个 (x, y) 的 noise，然后计算 alpha * img(x,y) + beta * noise(x,y), 这个过程叫做加噪声, 因为 noise 是纯随机生成, 所以 noise 的内容可以看作是正态分布的.  

重复这个加噪声的过程, 再重复了 n 次之后, 最终的结果会导致 img 的信息全部丧失, 只剩下了 noise  

现在定义重复 n 次加噪声之后的图像 noiseized-img = noiseize(img, t), 那么原图就是 noiseize(img, 0), 经过 10 次加噪声的图像就是 noiseize(img, 10)    

现在构建一个模型, 模型的 output 是 N(0,1) 的正态分布, 模型的 input 是 noiseize(img, t), 然后以 model 输出的噪声和 N(0, 1) 的差距作为优化目标, 就得到了 diffusion 模型  

```py
beta = [0.1, 0.2, 0.3 ... ] 

def noiseize(img, t, noise = None, depth):
    if t == depth:
        return img, noise
    if noise == None:
        noise = torch.randn_like(img)

    b = beta[depth]

    a = 1 - b

    return noiseize(
        a * img +  b * noise, 
        t, 
        noise, 
        depth + 1
    )

# 优化目标
def goal(model, img, t):
    noiseize_img, noise = noiseize(img, t)
    noise_pred = model(img, t)
    return F.l1_loss(noiseize_img, noise_pred)
```

其中 beta 数组的每一个元素表示每一次噪声的强度, 只要保证噪声强度随着每一次噪声都逐渐增加即可. 相比较 noiseize 的递归版本, noiseize 可以被优化成  

```py
beta = [0.1, 0.2, 0.3 ... ] 

# Pre-calculate different terms for closed form
alphas = 1. - betas

alphas_cumprod = torch.cumprod(alphas, axis=0)

alphas_cumprod_prev = F.pad(alphas_cumprod[:-1], (1, 0), value=1.0)

sqrt_recip_alphas = torch.sqrt(1.0 / alphas)

sqrt_alphas_cumprod = torch.sqrt(alphas_cumprod)

sqrt_one_minus_alphas_cumprod = torch.sqrt(1. - alphas_cumprod)

posterior_variance = betas * (1. - alphas_cumprod_prev) / (1. - alphas_cumprod)

def noiseize(img, t);
    sqrt_alphas_cumprod_t = sqrt_alphas_cumprod[t]

    sqrt_one_minus_alphas_cumprod_t = sqrt_one_minus_alphas_cumprod[t]

    # mean + variance
    return sqrt_alphas_cumprod_t * img + sqrt_one_minus_alphas_cumprod_t * noise, noise
```

# Link

[https://colab.research.google.com/drive/1sjy9odlSSy0RBVgMTgP7s99NXsqglsUL?usp=sharing#scrollTo=2fUPyJghdoUA](https://colab.research.google.com/drive/1sjy9odlSSy0RBVgMTgP7s99NXsqglsUL?usp=sharing#scrollTo=2fUPyJghdoUA)

[https://www.youtube.com/watch?v=a4Yfz2FxXiY&t=1274s&ab_channel=DeepFindr](https://www.youtube.com/watch?v=a4Yfz2FxXiY&t=1274s&ab_channel=DeepFindr)