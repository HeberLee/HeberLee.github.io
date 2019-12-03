---
layout:     post
title:      IOS之UITableView的优化
subtitle:   
date:       2019-03-12
author:     Heber
header-img: img/post-bg-miui6.jpg
catalog: true
tags:
    - IOS
    - UI基础
---


# 需要优化的方面

主要分两个方面，一是对cell的懒加载，二是cell的初始化方式

## cell的懒加载

UITableview里的单个cell并不是一开始就全部创建好的，只有当用户的屏幕滚动到这个cell所在的位置，它才会被创建，同时已经创建的cell会在屏幕滚过这个cell时被销毁。不过苹果已经为开发者预设了这个管理方式，无需另外操作。

## cell的初始化

在上面那个待优化方面中我们可以知道，在用户使用UITableview的时候，cell会频繁地创建和销毁，如果每次都是重新创建，必然有不小的负担，对此我们可以采用缓存池来解决这个问题。每当有cell需要销毁时，我们把这个cell扔到缓存池里，而不是直接销毁。每当要创建新的cell时，我们先对缓存池进行查询，看看有没有合适的旧cell，如果有合适的cell，对其进行稍加修改（例如文字和图标）之后放到UITableview中，只有当缓存池里没有合适的cell时，我们才直接创建一个新的cell。为了避免缓存池里的cell和我们想要的cell不匹配，我们会给每个cell标记一个tag，以此作为筛选的方式。

