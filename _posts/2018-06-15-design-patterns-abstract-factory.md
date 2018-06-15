---
layout: post
title: 设计模式：抽象工厂模式Abstract Factory
tags: [设计模式,php,design-patterns]
category: 设计模式
---
php抽象工厂模式的实现解释


## 解释
  抽象工厂模式可以看做是工厂模式的升级版。在不指定具体类的情况下创建一系列相关或依赖对象。 通常创建的类都实现相同的接口。 抽象工厂的客户并不关心这些对象是如何创建的，它只是知道它们是如何一起运行的。可以简单的理解为对一系列具有相同接口的工厂类添加约束。
  抽象工厂模式是用来约束工厂类的，多个工厂类具有相同的接口，在不确定产品详情时是很符合使用的。
  **引用**：抽象工厂模式（Abstract Factory Pattern）是围绕一个超级工厂创建其他工厂。该超级工厂又称为其他工厂的工厂。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。
在抽象工厂模式中，接口是负责创建一个相关对象的工厂，不需要显式指定它们的类。每个生成的工厂都能按照工厂模式提供对象。
## 实现
  假设我们有一个电子产品的工厂，我们工厂生产电脑、手机、手表等等电子产品
  ### 分析
  工厂生产电脑
  工厂生产手机
  工厂生产平板
  电脑有很多厂商
  手机有很多厂商
  平板有很多厂商
  
```php
/**
 * 抽象制作电子产品
 */
abstract class AbstractFactory
{
    abstract public function makeElectron($type, $model) {}
}
class ComputerFactory extends AbstractFactory
{
    public function makeElectron($brand)
    {
        return new Computer($brand);
    }
}
class PhoneFactory extends AbstractFactory
{
    public function makeElectron($brand)
    {
        return new Phone($brand);
    }
}
class IpadFactory extends AbstractFactory
{
    public function makeElectron($brand)
    {
        return new Ipad($brand);
    }
}

/**
 * 品牌
 */
abstract class Brand
{
    protected $brand;

    public function __construct($brand) 
    {
        $this->brand = $brand;
    }
}

class Computer extends Brand {

}
class Phone extends Brand {
    
}
class Ipad extends Brand {
    
}
```

laravel官网上面copy的例子简单实用

AbstractFactory.php
```php
<?php

namespace DesignPatterns\Creational\AbstractFactory;

/**
 * 在这种情况下，抽象工厂是创建一些组件的契约
 * 在 Web 中。 有两种呈现文本的方式：HTML 和 JSON
 */
abstract class AbstractFactory
{
    abstract public function createText(string $content): Text;
}
```
JsonFactory.php
```php
<?php

namespace DesignPatterns\Creational\AbstractFactory;

class JsonFactory extends AbstractFactory
{
    public function createText(string $content): Text
    {
        return new JsonText($content);
    }
}
```
HtmlFactory.php
```php
<?php

namespace DesignPatterns\Creational\AbstractFactory;

class HtmlFactory extends AbstractFactory
{
    public function createText(string $content): Text
    {
        return new HtmlText($content);
    }
}
```
Text.php
```php
<?php

namespace DesignPatterns\Creational\AbstractFactory;

abstract class Text
{
    /**
     * @var string
     */
    private $text;

    public function __construct(string $text)
    {
        $this->text = $text;
    }
}
```
JsonText.php
```php
<?php

namespace DesignPatterns\Creational\AbstractFactory;

class JsonText extends Text
{
    // 你的逻辑代码
}
```
HtmlText.php
```php
<?php

namespace DesignPatterns\Creational\AbstractFactory;

class HtmlText extends Text
{
    // 你的逻辑代码
}
```

Tests/AbstractFactoryTest.php
```php
<?php

namespace DesignPatterns\Creational\AbstractFactory\Tests;

use DesignPatterns\Creational\AbstractFactory\HtmlFactory;
use DesignPatterns\Creational\AbstractFactory\HtmlText;
use DesignPatterns\Creational\AbstractFactory\JsonFactory;
use DesignPatterns\Creational\AbstractFactory\JsonText;
use PHPUnit\Framework\TestCase;

class AbstractFactoryTest extends TestCase
{
    public function testCanCreateHtmlText()
    {
        $factory = new HtmlFactory();
        $text = $factory->createText('foobar');

        $this->assertInstanceOf(HtmlText::class, $text);
    }

    public function testCanCreateJsonText()
    {
        $factory = new JsonFactory();
        $text = $factory->createText('foobar');

        $this->assertInstanceOf(JsonText::class, $text);
    }
}
```