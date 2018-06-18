---
layout: post
category: php
tags: php
title: strtr和str_replace的效率
---
经测试后`str_replace`函数的效率最高，网上说`strtr`比`str_replace`快四倍的说法不可信。其实效率都几乎一样，另外php5.6以上版本`str_replace支持中文替换了`


## 效率测试
网上看到很多文章都说如果可用使用`strtr`时不要使用`str_replace `因为`strtr`比`str_replace `速度快四倍。所以特别测试记录一下。
### 环境
Mac pro 2.5 GHz Intel Core i7
MAMP集成环境 PHP7.1
### 字符串替换
首先测试了对单一字符串替换`120`个字符串
```
$str = 'UIRjcs0GMREpgUKUAAmZmPGR3mz8K7s1wUkZnpbX4HYc4dFD9rZub...';
```
每个函数各执行100次
```php
$time = microtime(true);
for ($i=0; $i < 100; $i++) { 
    strtr($str, 'v', 'a');
}
echo 'strtr: ',microtime(true) - $time;
$time = microtime(true);
for ($i=0; $i < 100; $i++) { 
    str_replace('v', 'a', $str);
}
echo '<br />str_replace: ',microtime(true) - $time;
```
结果：并没有什么区别
```
strtr:       0.0129399299622
str_replace: 0.0130231380463
```
#### 字符串数组替换
每个函数各执行100次
```php
$time = microtime(true);
for ($i=0; $i < 100; $i++) { 
    strtr($str, ['v'=>'a', 'b'=>'c']);
}
echo 'strtr: ',microtime(true) - $time;
$time = microtime(true);
for ($i=0; $i < 100; $i++) { 
    str_replace(['v', 'a', 'd', 'lsi', 'S'], ['b','c', 'a', 'jie', 's'], $str);
}
echo '<br />str_replace: ',microtime(true) - $time;
```
结果：其实差不多一样
```
strtr:       0.0133368968964
str_replace: 0.0133318901062
```
总结：看到东西要多测试测试，否则可能就被误导了。
我测试了中文替换，结果发展在`php 5.6`和`php 5.6`版本之后可以直接用`str_repalce`进行中文替换了。