---
layout:     post
title:      IOS之自动布局
subtitle:   
date:       2019-03-06
author:     Heber
header-img: img/post-bg-miui6.jpg
catalog: true
tags:
    - IOS
    - UI基础
---


# 自动布局的种类

主要三种，autoLayout、autoReSizing、autoSizeClasses，其中autoLayout、autoReSizing两者冲突，autoSizeClasses依赖autoLayout


# 约束的规则

1、左边距和上边距的优先级会大于右边距和下边距，也就是说如果同时添加这四个约束的同时，view的宽高也是固定的情况下，后两个其实是无效的。

2、对于同一层级的两个view之间的约束关系，添加到它们的父view上

3、对于不同层级的两个view之间的约束关系，添加到离他们最近的共同父view上

4、对于两个父子view之间的约束关系，添加到父view上。