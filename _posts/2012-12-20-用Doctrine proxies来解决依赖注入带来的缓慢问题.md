---
layout: post
title: "用Doctrine proxies来解决依赖注入带来的缓慢问题"
description: "Symonfy2引入了许多高级语言常用的设计模式等高级特征，进阶symfony，依赖注入（Dependency Injection）有时是个不可避免用来解决类间解耦的手段。"
category: PHP
tags: [方法思想]
---
Symonfy2引入了许多高级语言常用的设计模式等高级特征，进阶symfony，依赖注入（Dependency Injection）有时是个不可避免用来解决类间解耦的手段。

###依赖注入容器与其性能
依赖注入容器能给程序带来许多好处，它可以允许你组合多种复杂的对象图表（object graphs）而无须受限于一些没必要的丑陋方法(通常是静态方法)。

使用依赖注入容器你可以自动的获得一些解锁的好处：
####避免硬编码的依赖：
你的对象无须处理（初始化）它的一些依赖关系
####更好的“关注点分离”（Seperation of Concerns）：
跨对象的分离会变得更简单起来因为容器会帮助你很好的把他们粘合起来
####“模仿”（Mocking）变得更容易
当你进行单元测试（Unit testing）的时候，mock对象会变得很轻松，因为它会帮你解决组合实例依赖关系的问题

但它也有一个主要的缺点：因为对象不在自行管理初始化它的依赖对象关系了，__那么这时你的对象也许会建立一个庞大object graphs，即使你不完全使用到它们。__

让我们看下下面的例子：

	class B {}
	 
	class C {}
	 
	class D {
	    public function __construct(A $a, B $b, C $c)
	    {
	        // ...
	    }
	}
	 
	class HelloWorld
	{
	    public function __construct(D $d)
	    {
	        // ...
	    }
	 
	    public function sayHello()
	    {
	        return 'Hello World';
	    }
	}



{% include JB/setup %}
