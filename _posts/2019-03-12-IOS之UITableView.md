---
layout:     post
title:      IOS之UITableView
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

在上面那个待优化方面中我们可以知道，在用户使用UITableview的时候，cell会频繁地创建和销毁，如果每次都是重新创建，必然有不小的负担，对此我们可以采用缓存池来解决这个问题。每当有cell需要销毁时，我们把这个cell扔到缓存池里，而不是直接销毁。每当要创建新的cell时，我们先对缓存池进行查询，看看有没有合适的旧cell，如果有合适的cell，对其进行稍加修改（例如文字和图标）之后放到UITableview中，只有当缓存池里没有合适的cell时，我们才直接创建一个新的cell。为了避免缓存池里的cell和我们想要的cell不匹配，我们会给每个cell标记一个tag，以此作为筛选的方式,tag为静态变量，避免重复创建。

```
-(UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath{
	static NSString* TAG = @"test"; 
    UITableViewCell* cell = [tableView dequeueReusableCellWithIdentifier:@"a"];
    if(cell == nil){
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:TAG];
    }
    cell.textLabel.text = @"1";
    return cell;
}
```

# 自定义cell

之前我有提到在oc中自定义控件的创建方式，其中，在纯代码创建模式中，我把控件的view的构造和frame位置都写在initWithFrame这个方法中，但是我上面有写到，UITableview的cell是用initWithStyle来创建的，并且，initWithStyle这个方法并不会去调用initWithFrame方法，所以我们需要把cell的view的构造和frame位置都写在initWithStyle中而不是写在initWithFrame中
```
- (instancetype)initWithStyle:(UITableViewCellStyle)style reuseIdentifier:(NSString *)reuseIdentifier{
    if(self = [super initWithStyle:style reuseIdentifier:reuseIdentifier]){
        UIImageView* iconImageView = [[UIImageView alloc] init];
        self.iconImageView = iconImageView;
        [self.contentView addSubview:self.iconImageView];
        
        UILabel* titleLabel = [[UILabel alloc] init];
        
        self.titleLabel = titleLabel;
        [self.contentView addSubview:self.titleLabel];
    }
    return self;
}

- (void)layoutSubviews{
    [super layoutSubviews];
    self.titleLabel.frame = CGRectMake(10, 10, 100, 20);
}
```