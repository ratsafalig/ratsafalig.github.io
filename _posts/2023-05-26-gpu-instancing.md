---
title: Batching 技术 和 GPU Instancing 技术
tags:
- Game
- GL
- Unity
categories:
- Game
- GL
- Unity
image:
    path: /assets/img/2023-05-26-gpu-instancing/gpu.png
---

## Batching

场景里有很多 mesh 的时候, 性能下降的主要原因之一是 draw-call 过多, 如果对于每一个 mesh 都要进行一次 draw-call 性能消耗非常大.  

这个时候如果多个 mesh 使用相同的 material, 原理上可以把所有相同材质的 mesh 看成一个大 mesh, 然后只进行一次 draw-call 就把这些 mesh 的所有 vertices 和 indices 都画出来  

这个过程就叫 batching, 通过 bake 一个大的 mesh 来只进行一次 draw-call, 但 batching 的所有物体必须是同一个 material 的才行

### Batching Off

不同材质的 mesh, unity 采用了两次 draw-call 来完成绘制  

![](/assets/img/2023-05-26-gpu-instancing/frame_0.png)

### Batching On

相同材质的 mesh, unity 采用了一次 draw-call 就完成了绘制

![](/assets/img/2023-05-26-gpu-instancing/frame_1.png)

## GPU Instancing

GPU Instancing 通常用在同样 mesh 同样材质的物体渲染上, 例如渲染一大堆的相同物体 ( TRS 矩阵可以不同 )  

因为 material 和 mesh 都相同, GPU 可以在很大的部分进行缓存 ( 例如 顶点数据, 索引数据, 材质数据 的 send-in ), 让一个 draw-call 更快来实现优化  

对比 batching, 因为不需要对 mesh 做合并, 某种程度上对 CPU 压力更小  

### Graphics.DrawMeshInstanced

Graphics.DrawMeshInstanced 提供了一种手动使用 GPU-Instanced 的方法, 代码如下  

![](/assets/img/2023-05-26-gpu-instancing/gpu.png)

```cs
using UnityEditor;
using UnityEngine;
using System.Collections.Generic;

[ExecuteAlways]
public class MeshCreator : MonoBehaviour {
    public Mesh mesh;

    public int instance = 1000;

    public Material mat;

    public List<Matrix4x4> matrices;

    void OnEnable(){
        matrices = new List<Matrix4x4>();
        
        for(int i = 0;i < instance;i++){
            
            float x = Random.Range(-100, 100);
            float y = Random.Range(-100, 100);
            float z = Random.Range(-100, 100);

            matrices.Add(Matrix4x4.TRS(new Vector3(x,y,z), Quaternion.identity, Vector3.one));
        }
    } 

    public void CreateMesh(){
        if(mesh != null && mat != null && matrices.Count != 0){
            Debug.Log("CreateMesh");
            Graphics.DrawMeshInstanced(mesh, 0, mat, matrices);
        }
    }

    void Update(){
        CreateMesh();
    }
}
```

## Link

[GPU_Instancer:Terminology](https://wiki.gurbu.com/index.php?title=GPU_Instancer:Terminology)