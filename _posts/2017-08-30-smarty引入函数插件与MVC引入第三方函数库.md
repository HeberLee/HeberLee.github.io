---
layout:     post
title:      smarty引入函数插件与MVC引入第三方函数库
subtitle:   三种函数插件与smarty函数库的引入
date:       2017-08-30
author:     Heber
header-img: img/post-bg-hacker.jpg
catalog: true
tags:
    - MVC
    - smarty
---


## function函数插件的使用
1.在smarty\smarty\plugins文件夹中新建一个名为function.test.php的文件，在其中定义想要使用的函数,名字为smarty_function_test。
2.在smarty的tpl文件夹里新建一个tpl文件来调用函数，格式与普通function函数相同
3.在smarty主文件里利用display来调用tpl文件
4.访问主文件


## modifier函数插件的使用
1.在smarty\smarty\plugins文件夹中新建一个名为modifier.test.php的文件，在其中定义想要使用的函数,名字为smarty_modifiler_test。
2.在smarty的tpl文件夹里新建一个tpl文件来调用函数，格式与调用变量调节器相同
3.在smarty主文件里利用display来调用tpl文件
4.访问主文件


## block区块函数插件的使用
1.在smarty\smarty\plugins文件夹中新建一个名为block.test.php的文件，在其中定义想要使用的函数,名字为smarty_block_test。
2.在smarty的tpl文件夹里新建一个tpl文件来调用函数，格式与正常调用区块函数相同
3.在smarty主文件里利用display来调用tpl文件
4.访问主文件

##MVC引入第三方函数库(以smarty为例)
1.复制smarty文件到MVC/libs/ORG目录下
2.在function文件中添加新建第三方函数库对象的方法

```objc
function ORG($path, $name, $params=array()){
    require_once('libs/ORG/'.$path.$name.'.class.php');
    $obj = new $name();
    if (!empty($params)) {
      foreach ($parames  as $key => $value) {
        $obj->$key = $value;
      }
    }
    return $obj;
```
3.为了方便可将参数写入config文件并从index引入，然后就可以使用第三方函数库了


