---
title: AI生成动画帧的一次尝试
tags:
- AI
- Game
categories:
- AI
- Game
---

# 工具

checkpoints: delibrate_v2.safetensors
lora: Small_Monstersv2
textual inversion: mechasoulall
[https://www.remove.bg/zh/upload](https://www.remove.bg/zh/upload)

# 流程

# 第一步

prompt 是 `mantis  mechasoulall <lora:Small_Mostersv2:1> `
用 controlnet 参数  

![](/assets/img/2023-05-19-ai-animation/first_controlnet.png)

这一步生成的结果如下  

![](/assets/img/2023-05-19-ai-animation/first.png)

controlnet 使用的基准图是 

![](/assets/img/2023-05-19-ai-animation/controlnet.png)  

这张图也是拿AI生成的, 或者也可以直接上网搜一个

# 第二步

把图传到 image2image, 找一张合适的 pose, 用 openpose controlnet 生成动画的开始帧数  
因为我要做一个格斗动画, 所以我使用了侧面站立的图  

使用的 prompt 还是 `mantis  mechasoulall <lora:Small_Mostersv2:1>`  

使用的 controlnet 参数  

![](/assets/img/2023-05-19-ai-animation/second_controlnet.png)  

这一步得到的图像是  

![](/assets/img/2023-05-19-ai-animation/second.png)  

这个大概是我想要的开始帧数动作, 下载下来图片, 去掉背景, 得到  

![](/assets/img/2023-05-19-ai-animation/download.png)  ( 这里我换了一张图片, 也是AI生成的 )  

# 第三步  

把无背景的图片上传到 inpaint, 看到上面去掉背景的图少了手臂, 重绘一下手臂.  

这一步不要 controlnet, prompt 还是一样 `mantis  mechasoulall <lora:Small_Mostersv2:1>` 

![](/assets/img/2023-05-19-ai-animation/inpaint.png)  

得到的图像是  

![](/assets/img/2023-05-19-ai-animation/frame_0.png)  

这就是第一帧的图片  

# 后续  

接下来的步骤是重复把第一帧的图片用 sketch inpaint 修改大致的动作, 制作出第二帧  

![](/assets/img/2023-05-19-ai-animation/frame_1.png)


