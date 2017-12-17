---
layout:     post
title:      "游戏角色移动"
subtitle:   "碰撞检测"
date:       2017-09-15 20:00:00
author:     "Iteevo"
header-img: "img/in-post/CollsionAvoidance/2017_09_15.jpg"
header-mask: 0.3
catalog:    true
tags:
    - game AI
    - C#
---

> 本文首发于 [Iteevo Blog](http://iteevo.com/2017/09/15/Collision-Avoidance) 转载请保留链接。

# 碰撞检测

游戏场景中很多运动的角色，为了避免角色在运动期间相互穿插对方，我们需要做碰撞检测。一般的做法是检测当前角色与其它角色之间是否会发生碰撞，如果有可能发生碰撞，就要避让最短时间内会碰撞的角色。在以下代码中采用的是靠右行驶原则，选择碰撞点右边的一个零界点作为当前角色运动的中间目标点。

```
public class CollisionAvoidance : MonoBehaviour {
    //public Transform[] candidates;
    public Seek MySeek;
    public float detectRadius = 6f;
    public float radius = 1;
    public Vector3 vel ;
	// Use this for initialization
	void Start () {
        MySeek = GetComponent<Seek>();
	}
	
	// Update is called once per frame
	void Update () {
        float shortTime = float.MaxValue;
        Collider[] candidates = Physics.OverlapSphere(transform.position, detectRadius,1<<LayerMask.NameToLayer("Entity"));
        CollisionAvoidance target = null;
        for (int i = 0; i < candidates.Length;i++)
        {
            if (candidates[i].gameObject == gameObject)
                continue;
            CollisionAvoidance ad = candidates[i].GetComponent<CollisionAvoidance>();
            Vector3 deltaVel = ad.vel - vel;
            Vector3 dis = candidates[i].transform.position - transform.position;
            if (Vector3.Dot(deltaVel, dis) < 0)
            {
                float time = dis.magnitude / Vector3.Project(deltaVel, dis).magnitude;
                if (time < shortTime)
                {
                    shortTime = time;
                    target = ad;
                }
            }
        }
        if (shortTime < float.MaxValue)
        {
            Vector3 posA = target.transform.position + target.vel * shortTime;
            Vector3 posB = transform.position + vel * shortTime;
            if ((posA - posB).sqrMagnitude < radius * radius)
            {
                MySeek.TargetPos = posB + Vector3.Cross(Vector3.up, vel) * radius;
            }
        }
        else
        {
                MySeek.TargetPos = vel * 2f + transform.position;
        }

	}
}
```



