---
title: OpenGL 矩阵
tag:
- GL
- Game
---

正常情况下 3 * 3 矩阵已经足够表现 3d 空间内的线性变换  
但线性变换有两个前提  

1. 原点在线性变换后还是原点  
2. 任何直线在线性变换后还是直线  

但 opengl 不仅仅需要线性变换, 比如  

1. 平移变换  
2. 投影变换  
3. 旋转变换  

```
[ 1, 0, 0, x ]
[ 0, 1, 0, y ]
[ 0, 0, 1, z ]
[ 0, 0, 0, 1 ]

矩阵将坐标平移 (x, y, z)  
```

所以需要定义第四个分量 w ( 齐次坐标 ),  
当 w != 1 的时候, 需要将向量 / w  

```
(x*w, y*w, z*w, w) / w = (x, y, z, 1)  
```  

# MVP 矩阵  

在 opengl 里有几个坐标系  

```
model pos: 模型建模的坐标  
world pos: 模型在世界里的位置坐标
camera pos: 玩家眼睛的位置
view dir: 玩家眼睛看向的方向  
```

所以把一个物体 ( model ) 转换到屏幕上需要做几次坐标转换  
这个坐标转换的过程通过乘以一个 MVP ( model view projection ) 矩阵来达到  

```glsl
// position 模型坐标变换
// model 世界坐标变换
// view 摄像机坐标变换
// proj 投影矩阵
void main() {
    gl_Position = proj * view * model * vec4(position, 1.0);
}
```

# Model Matrix

model 矩阵可以通过简单的坐标转换得到  

# View Matrix

view 矩阵需要 camera 的位置和 view-dir来计算 (实际上还需要一个 up 向量, 来标识 camera 的 z 轴是哪个方向)  
up 向量和 view-dir 是新坐标系的 z, x 轴, camera-pos 是新坐标系的原点  
所以 view 矩阵是一个坐标轴变换 + 旋转的矩阵  

# Projection Matrix

projection 矩阵把 camera 投影到屏幕空间  

取决于投影方式, 投影方式有 透视投影 和 正交投影  

![](/assets/img/2021-01-01-why-opengl-using-4-d-matrix/perspective.png)

![](/assets/img/2021-01-01-why-opengl-using-4-d-matrix/orth.png)

project 矩阵的构造方法详见 Link  

# Link

[tutorial-3-matrices](http://www.opengl-tutorial.org/beginners-tutorials/tutorial-3-matrices/)

[NDC](https://zhuanlan.zhihu.com/p/65969162)

[投影矩阵](https://www.zhihu.com/tardis/zm/art/73034007?source_id=1003)

[understanding-screen-position-node-in-unity-shader-graph](https://gamedev.stackexchange.com/questions/186226/understanding-screen-position-node-in-unity-shader-graph)

[opengl-perspective-projection-matrix](https://www.scratchapixel.com/lessons/3d-basic-rendering/perspective-and-orthographic-projection-matrix/opengl-perspective-projection-matrix.html)