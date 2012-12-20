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

但它也有一个主要的缺点：因为对象不在自行管理初始化它的依赖对象关系了，那么这时你的对象也许会建立一个庞大object graphs，即使你不完全使用到它们。

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

上述代码经常出现于MVC的控制器中，你可能有更多的action（如上面的HelloWorld），但它们都没有用来处理依赖关系。

可能你也发现了，调用`HelloWorld#sayHello()`，我们需要初始化5个对象：`A`, `B`, `C`, `D`, `HelloWorld`。

然而这样过于“健壮”的代码会让我们在进行单元测试时很难将它们剥离出来，这会带来性能问题。
当其中的一些对象会寻找一些资源或者执行一些昂贵的操作时，性能问题会体现的额外明显：比如打开文件，用socket到一个远程服务器。

所以纯粹的使用依赖注入虽然会使得代码更好维护，健壮，但也带来不少性能上的缺陷，特别在PHP,每次分发请求时，每个object graph都会重建（不使用缓存的情况下）。

###Doctrine Proxies来拯救！
Symfony中经常使用Doctrine Proxies类来加载实体（Entity）的映射关系。比如一个`学生`对象（可看作一条表记录），存储了一个班级的映射关系，那么当我们这么获取一个学生对象时：

	$student_xiaoming = $em->getEntityManager()->getRepository('bundle:Student')->find(1);

打印`$student_xiaoming`会发现，班级信息部分的类型为`Doctrine Proxies`。



{% include JB/setup %}
