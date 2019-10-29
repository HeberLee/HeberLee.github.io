---
layout:     post
title:      IOS之kvc与kvo
subtitle:   
date:       2019-03-04
author:     Heber
header-img: img/post-bg-miui6.jpg
catalog: true
tags:
    - IOS
---


#KVC——key value coding（键值编程）

1.通过kvc方式赋值的变量在输出时能够提供自动类型转换，如int=>float

2.kvc的赋值方式
```
第一种
	[对象 setValue:@"值" forKey:@"键"];
第二种，如果需要对对象的子对象的某个属性赋值
	[对象.子对象 setValue:@"值" forKey:@"键"]；
	或者
	[对象 setValue:@"值" forKeyPath:@"子对象.键"];
```

3.kvc可以直接修改对象的私有成员变量

4.kvc可以直接使用setValuesForKeyWithDictionary将与类中变量一一对应的字典直接赋值给类对象，不过灵活性非常差，不建议使用。

5.kvc可以使用valueForKeyPath取出对象数组里所有对象的某个键对应的值。

#KVO——key value observing（键值监听）

1.kvo就是监听键值对的改变，通常与scollview之类的控件配合。

2.使用addObserver来新增对某个键值的监听器。同时配合observeValueForKeyPath来执行监听到键值改变后的行为。