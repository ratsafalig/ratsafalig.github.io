---
title: AI生成动画帧的第二次尝试
tags:
- AI
- Game
categories:
- AI
- Game
---

第一次尝试思路是 使用 control-net 生成第一帧, 动过 photoshop 稍微修改然后扔进 inpaint 去生成第二帧  
这一次尝试使用多个pose结合成的 controlnet open-pose 一次性生成多个 pose 然后直接拼接  

![](/assets/img/2023-05-24-ai-animation-second-try/openpose.png)

![](/assets/img/2023-05-24-ai-animation-second-try/openpose.mp4)