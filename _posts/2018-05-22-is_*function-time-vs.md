---
layout: post
title: is_string instanceof is_array is_int is_float is_object is_*系列函数的效率
tags: [php]
category: php
---
结果显示不管判断的是字符串、整数、对象、数组..其实效率都不差什么的


### 测试环境
Mac pro 2.5 GHz Intel Core i7
MAMP 集成缓存 php7.1

### 测试细节
每个函数通过for循环执行`1000次`然后得到结果。
其中测试过各种变量类型
#### 小问题
发现了一个小问题，在执行到第一个循环体时使用的时间比之后执行的循环所用到的时间多一点
我首先第一个测试的函数是`is_string`结果显示`is_string: is_string: 0.000280141830444`所有我不得不在后面在防止一个`is_string函数的测试`
### 测试结果
```
is_array: 0.00023889541626
is_float: 0.000263214111328
is_int: 0.00026798248291
is_null: 0.000239133834839
is_bool: 0.000220060348511
is_object: 0.000250101089478
is_numeric: 0.000922918319702
instanceof: 0.000236034393311
is_string: 0.000236988067627
```
### 结论
其实如果用`if判断`的话，使用`instanceof`操作符会稍微的快一点。
`is_numeric`的效率是最差劲的，所以能找到其他类型判断函数代替最好