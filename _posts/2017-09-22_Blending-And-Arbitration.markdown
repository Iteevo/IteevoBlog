---
layout:     post
title:      "组合游戏角色移动"
subtitle:   "SteerBehavior混合和仲裁"
date:       2017-09-22 20:00:00
author:     "Iteevo"
header-img: "img/in-post/BlendingAndArbitration/2017_09_22.jpg"
header-mask: 0.3
catalog:    true
tags:
    - game AI
    - C#
---

> 本文首发于 [Iteevo Blog](http://iteevo.com/2017/09/23/Blending_And_Arbitration) 转载请保留链接。

#SteerBehavior混合和仲裁


通过组合基本steerBehavor行为，我们可以实现更加复杂的运动。通常有两种组合方式：混合和仲裁。
## Weighted Blending

使用混合权重来组合Steering Behavior是最简单的方式。比如我们的角色们需要彼此靠近，但又不能彼此有交叉和重合，那么我们必须同时考虑flee和seek两种基本行为。基本行为的权重要根据角色间的距离而变化。
    for behavior in behaviors
        steering += behavior.weight * behavior.behavior.getSteering()

## Priority Based
![](/img/in-post/BlendingAndArbitration/priorityBased.png)
上图所示的复杂场景中，基于权重的行为组合就会失效。这时我们就需要给予优先级来混合行为。
    for group in groups:
      steering = group.getSteering()
      if steering.linear.length() > epsilon or
         abs(steering.angular) > epsilon:
        return steering




