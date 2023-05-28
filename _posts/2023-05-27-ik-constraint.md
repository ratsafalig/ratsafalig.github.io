---
title: Unity 反向动力 ( IK )
tags:
- Unity
- Game
categories:
- Unity
- Game
image:
    path: /assets/img/2023-05-27-ik-constraint/crab.gif
---

## Multi-Aim Constraint 

![](/assets/img/2023-05-27-ik-constraint/multi-arim.gif)

![](/assets/img/2023-05-27-ik-constraint/multi-aim.png)

## Two Bone Constraint

![](/assets/img/2023-05-27-ik-constraint/two-bone.gif)

![](/assets/img/2023-05-27-ik-constraint/two-bone.png)

### 例子

![](/assets/img/2023-05-27-ik-constraint/cube-two-bone.gif)

![](/assets/img/2023-05-27-ik-constraint/cube-two-bone.png)

## procedural animation

实现蜘蛛爬的算法实现:  

- 4 个 two-bone-ik 的脚当作蜘蛛的四个脚, 分别固定到各自的 target, 像这样

![](/assets/img/2023-05-27-ik-constraint/spider1.gif)

- 移动蜘蛛的时候, 判断每只脚移动的距离, 如果超过了必须走一步的距离, 开启一个 coroutine, 移动这只脚

![](/assets/img/2023-05-27-ik-constraint/crab.gif)

SpiderProceduralAnimation.cs

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SpiderProceduralAnimation : MonoBehaviour
{
    public Transform[] legTargets;
    public float stepSize = 1f;
    public int smoothness = 1;
    public float stepHeight = 0.1f;
    public bool bodyOrientation = true;

    private float raycastRange = 1f;
    private Vector3[] defaultLegPositions;
    private Vector3[] lastLegPositions;
    private Vector3 lastBodyUp;
    private bool[] legMoving;
    private int nbLegs;
    
    private Vector3 velocity;
    private Vector3 lastVelocity;
    private Vector3 lastBodyPos;

    private float velocityMultiplier = 15f;

    static Vector3[] MatchToSurfaceFromAbove(Vector3 point, float halfRange, Vector3 up)
    {
        Vector3[] res = new Vector3[2];
        RaycastHit hit;
        Ray ray = new Ray(point + halfRange * up, - up);
        
        if (Physics.Raycast(ray, out hit, 2f * halfRange))
        {
            res[0] = hit.point;
            res[1] = hit.normal;
        }
        else
        {
            res[0] = point;
        }
        return res;
    }
    
    void Start()
    {
        lastBodyUp = transform.up;

        nbLegs = legTargets.Length;
        defaultLegPositions = new Vector3[nbLegs];
        lastLegPositions = new Vector3[nbLegs];
        legMoving = new bool[nbLegs];
        for (int i = 0; i < nbLegs; ++i)
        {
            defaultLegPositions[i] = legTargets[i].localPosition;
            lastLegPositions[i] = legTargets[i].position;
            legMoving[i] = false;
        }
        lastBodyPos = transform.position;
    }

    IEnumerator PerformStep(int index, Vector3 targetPoint)
    {
        Vector3 startPos = lastLegPositions[index];
        for(int i = 1; i <= smoothness; ++i)
        {
            legTargets[index].position = Vector3.Lerp(startPos, targetPoint, i / (float)(smoothness + 1f));
            legTargets[index].position += transform.up * Mathf.Sin(i / (float)(smoothness + 1f) * Mathf.PI) * stepHeight;
            yield return new WaitForFixedUpdate();
        }
        legTargets[index].position = targetPoint;
        lastLegPositions[index] = legTargets[index].position;
        legMoving[0] = false;
    }


    void FixedUpdate()
    {
        velocity = transform.position - lastBodyPos;
        velocity = (velocity + smoothness * lastVelocity) / (smoothness + 1f);

        if (velocity.magnitude < 0.000025f)
            velocity = lastVelocity;
        else
            lastVelocity = velocity;
        
        
        Vector3[] desiredPositions = new Vector3[nbLegs];
        int indexToMove = -1;
        float maxDistance = stepSize;
        for (int i = 0; i < nbLegs; ++i)
        {
            desiredPositions[i] = transform.TransformPoint(defaultLegPositions[i]);

            float distance = Vector3.ProjectOnPlane(desiredPositions[i] + velocity * velocityMultiplier - lastLegPositions[i], transform.up).magnitude;
            if (distance > maxDistance)
            {
                maxDistance = distance;
                indexToMove = i;
            }
        }
        for (int i = 0; i < nbLegs; ++i)
            if (i != indexToMove)
                legTargets[i].position = lastLegPositions[i];

        if (indexToMove != -1 && !legMoving[0])
        {
            Vector3 targetPoint = desiredPositions[indexToMove] + Mathf.Clamp(velocity.magnitude * velocityMultiplier, 0.0f, 1.5f) * (desiredPositions[indexToMove] - legTargets[indexToMove].position) + velocity * velocityMultiplier;
            Vector3[] positionAndNormal = MatchToSurfaceFromAbove(targetPoint, raycastRange, transform.up);
            legMoving[0] = true;
            StartCoroutine(PerformStep(indexToMove, positionAndNormal[0]));
        }

        lastBodyPos = transform.position;
        if (nbLegs > 3 && bodyOrientation)
        {
            Vector3 v1 = legTargets[0].position - legTargets[1].position;
            Vector3 v2 = legTargets[2].position - legTargets[3].position;
            Vector3 normal = Vector3.Cross(v1, v2).normalized;
            Vector3 up = Vector3.Lerp(lastBodyUp, normal, 1f / (float)(smoothness + 1));
            transform.up = up;
            lastBodyUp = up;
        }
    }

    private void OnDrawGizmosSelected()
    {
        for (int i = 0; i < nbLegs; ++i)
        {
            Gizmos.color = Color.red;
            Gizmos.DrawWireSphere(legTargets[i].position, 0.05f);
            Gizmos.color = Color.green;
            Gizmos.DrawWireSphere(transform.TransformPoint(defaultLegPositions[i]), stepSize);
        }
    }
}

```

SpiderController.cs

一个简单的 Input Controller 脚本  

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[RequireComponent(typeof(Rigidbody))]
public class SpiderController : MonoBehaviour
{
    public float _speed = 1f;

    private Rigidbody _rigidbody;

    // Start is called before the first frame update
    void Start()
    {
        _rigidbody = GetComponent<Rigidbody>();
    }

    // Update is called once per frame
    void FixedUpdate()
    {
        float multiplier = 1f;
        if (Input.GetKey(KeyCode.LeftShift))
            multiplier = 2f;

        if (_rigidbody.velocity.magnitude < _speed * multiplier)
        {

            float value = Input.GetAxis("Vertical");
            if (value != 0)
                _rigidbody.AddForce(0, 0, value * Time.fixedDeltaTime * 1000f);
            value = Input.GetAxis("Horizontal");
            if (value != 0)
                _rigidbody.AddForce(value * Time.fixedDeltaTime * 1000f, 0f, 0f);
        }
    }
}

```

## Link

[SpiderProceduralAnimation](https://github.com/lchaumartin/SpiderProceduralAnimation/tree/FirstVideo)

[Unity-Procedural-IK-Wall-Walking-Spider](https://github.com/PhilS94/Unity-Procedural-IK-Wall-Walking-Spider)