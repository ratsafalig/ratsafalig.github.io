---
title: 安卓手机相机控制
tags:
- Game
- Unity
categories:
- Game
- Unity
---

## CameraController.cs

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.EventSystems;
using TouchScript.Gestures.TransformGestures;

public class CameraController : MonoBehaviour
{
    [SerializeField]
    float offsetDistance;
    [SerializeField]
    float offsetHeight;
    //
    [SerializeField]
    Transform dstTransform;
    [SerializeField]
    Vector3 velocityPos = new Vector3(.1f, .1f, .1f);
    [SerializeField]
    Vector3 velocityRot = new Vector3(.1f, .1f, .1f);
    [SerializeField]
    private float smoothTimePos = 3.0f;
    [SerializeField]
    private float smoothTimeRot = 0.3f;
    [SerializeField]
    private Vector3 up;
    [SerializeField]
    private ScreenTransformGesture OneFingerMoveGesture;

    enum CameraType{
        LookAt,
        Touch,
    }

    [SerializeField]
    private Car car;

    private void OnEnable()
    {
        OneFingerMoveGesture.Transformed += oneFingerTransformHandler;
    }

    private void OnDisable()
    {
        OneFingerMoveGesture.Transformed -= oneFingerTransformHandler;
    }

    // Start is called before the first frame update
    void Start()
    {
        up = transform.up;
    }

    // Update is called once per frame
    void Update()
    {
        if(OneFingerMoveGesture.ActivePointers.Count != 0){
            UpdateTouch();
        }else{
            UpdatePosition();
            UpdateRotation();
        }
    }

    float velocityPosThreshold = .001f;
    float velocityRotThreshold = .001f;

    void UpdatePosition(){
        if(dstTransform == null){
            return;
        }

        Vector3 dirDistance = -dstTransform.forward;

        dirDistance.y = 0;

        Vector3 offsetDistanceV = dirDistance * offsetDistance;

        Vector3 offsetHeightV = new Vector3(0, offsetHeight, 0);

        Vector3 dstPos = dstTransform.position + offsetDistanceV + offsetHeightV;

        Vector3 position = Vector3.SmoothDamp(transform.position, dstPos, ref velocityPos, smoothTimePos);
        
        if(velocityPos.magnitude < velocityPosThreshold){
            return;
        }
        
        transform.position = position;
    }
    
    void UpdateRotation(){
        if(dstTransform == null){
            return;
        }

        Vector3 srcForward = transform.forward;

        Vector3 dstForward = dstTransform.forward;

        Vector3 forward = Vector3.SmoothDamp(srcForward, dstForward, ref velocityRot, smoothTimeRot);

        if(velocityRot.magnitude < velocityRotThreshold){
            return;
        }
        
        transform.up = up;

        transform.forward = forward;
    }

    void UpdateTouch(){
        // Vector3 rotation = transform.rotation.eulerAngles;

        // Vector3 dest = new Vector3(0, rotation.y, 0);

        Vector3 forward = transform.forward;

        Debug.DrawRay(transform.position, forward, Color.red, 5);

        car.OnTurn(forward);
    }

    public float PanSpeed = 10f;
    private void oneFingerTransformHandler(object sender, System.EventArgs e)
    {
        Vector3 deltaPos = OneFingerMoveGesture.DeltaPosition;

        Vector3 delta = (deltaPos * PanSpeed);

        // Debug.Log("oneFingerTransformHandler delta: " + delta + " deltaPos: " + deltaPos);

        delta = new Vector3(0, delta.x, 0) + new Vector3(-delta.y, 0, 0);

        Vector3 original = transform.rotation.eulerAngles;

        Vector3 dest = original + delta;

        transform.rotation = Quaternion.Euler(dest);
    }
}

```

## Car.cs

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Car : MonoBehaviour
{
    [SerializeField]
    Animator animator;

    [SerializeField]
    public float power = 0;
    [SerializeField]
    float powerSpeed = 50f;
    [SerializeField]
    bool hold = false;

    Rigidbody rigidbody;

    void OnEnable(){
        rigidbody = GetComponent<Rigidbody>();
    }

    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void FixedUpdate()
    {
        if(hold){
            OnHold();
        }

        Vector3 velocity = rigidbody.velocity;

        if(velocity.magnitude != 0){
            // is moving;
        }
    }

    public void OnSlide(){
        
    }

    public void OnHold(){
        power += powerSpeed * Time.deltaTime;
    }
    
    public void OnPress(){
        animator.SetTrigger("press");
        power = 0;
        hold = true;
    }

    public void OnRelease(){
        animator.SetTrigger("release");
        hold = false;

        Launch();
    }

    public void Launch(){
        rigidbody.AddForce(power * transform.forward.normalized, ForceMode.Impulse);
    }

    public void OnDead(){
        transform.position = Vector3.zero;
    }
    [SerializeField]
    private float rotThreshold = .1f;
    [SerializeField]
    private float rotSpeed = .01f;
    public void OnTurn(Vector3 dest){
        Vector3 original = transform.forward;

        Debug.DrawRay(transform.position, original, Color.green, 5);

        float singleStep = rotSpeed;

        float distance = Vector3.Angle(original, dest);

        Vector3 Ndest = Vector3.RotateTowards(original, dest, singleStep, 0.0f);

        transform.rotation = Quaternion.LookRotation(Ndest);

        Vector3 euler = transform.rotation.eulerAngles;

        euler.x = 0;
        euler.z = 0;

        transform.rotation = Quaternion.Euler(euler);
    }

    public Vector3 CalculateClosestRotation(Vector3 original){
        float x = original.x;
        float y = original.y;
        float z = original.z;

        Vector3 dest = new Vector3();

        dest.x = CalculateClosestRotationFloat(x);
        dest.y = CalculateClosestRotationFloat(y);
        dest.z = CalculateClosestRotationFloat(z);

        return dest;
    }

    public float CalculateClosestRotationFloat(float src){
        float result = src % 360;
        if(Mathf.Abs(result) > 180){
            if(result > 0){
                result = -(360 - Mathf.Abs(result));
            }else{
                result = 360 - Mathf.Abs(result);
            }
        }
        return result;
    }
}

```