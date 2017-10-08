---
layout:     post
title:      "GameAI中的角色移动"
subtitle:   "移动的基本组成和运用"
date:       2017-09-08 20:00:00
author:     "Iteevo"
header-img: "img/in-post/post-eleme-pwa/eleme-at-io.jpg"
header-mask: 0.3
catalog:    true
tags:
    - game AI
    - C#
---
<br><br>
> 本文首发于 [Iteevo Blog](http://iteevo.com/2017/09/08/Movement-in-GameAI/) 转载请保留链接。

角色的运动是AI最基本的需求，运动算法需要解决角色下一步的位置和朝向。
## Seek,Align,velocity 是移动算法最基本的三种组成形式？
### 1.Seek行为将当前角色的位置匹配到目标点。
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Seek : MonoBehaviour {
    public Vector3 TargetPos = 100*Vector3.forward;
	
	// Update is called once per frame
	void Update () {
        transform.position += (TargetPos - transform.position).normalized * Time.deltaTime;
	}
}
```

### 2.Align行为将角色的朝向和目标方向一致。
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Align : MonoBehaviour {
    public float TargetAngle = 60f;//顺时针绕z轴正方向的角度
	// Use this for initialization
	void Start () {
		
	}
	
	// Update is called once per frame
	void Update () {
        Quaternion target = Quaternion.Euler(Vector3.up * TargetAngle);
        transform.rotation = Quaternion.Lerp(transform.rotation, target, Time.deltaTime);//
	}
}
```
### 3.velocity行为将角色的运动匹配到目标速度，可以在接近目标速度的时候减速
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class VelocityMatch : MonoBehaviour {
    public float timeToTargetSpeed;
    public Vector3 targetVelocity;
    public Vector3 selfVelocity;
    public float maxAcceleration;
	// Use this for initialization
	void Start () {
		
	}
	
	// Update is called once per frame
	void Update () {
        Vector3 delta = targetVelocity - selfVelocity;
        float Acceleration = Mathf.Min(maxAcceleration,(delta/timeToTargetSpeed).magnitude);
        selfVelocity += Acceleration * Time.deltaTime*delta.normalized;
	}
}
```



