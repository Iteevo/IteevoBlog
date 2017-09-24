---
layout:     post
title:      "游戏人工智能简介"
subtitle:   "游戏人工智能基本概念和组成"
date:       2017-09-01 20:00:00
author:     "Iteevo"
header-img: "img/in-post/post-eleme-pwa/eleme-at-io.jpg"
header-mask: 0.3
catalog:    true
tags:
    - game AI
    - C#
---

> 本文首发于 [Iteevo Blog](http://iteevo.com/2017/09/01/introduction-to-gameAI/) 转载请保留链接。

## What is game AI？

游戏人工智能是让游戏世界中的角色表现出人类一样的思考能力和行为。游戏人工智能需要满足三个基本的需求：移动角色，决策要移动的目的地，如何有策略的思考。

## Model of Game AI 
![](/img/in-post/Introduction_to_game_AI/AI_Model.png)

## 实现游戏AI需要的三种关键元素：算法，数据结构和游戏世界的表现方式

### 1.算法(algorithms)是一步步地解决AI问题的过程，比如生成移动到目标的路径，决定拦截逃跑的敌人的移动方向，决策角色下一步要做的动作等等。
### 2.数据结构是算法的另一面，数据结构为我们的算法保存提供数据，而数据与游戏世界的表现息息相关。
###3.游戏世界的表现方式决定了我们怎么讲游戏世界的内容转化成AI算法能处理的数据，比如世界是用正方形的网格存储还是导航网格。

##

