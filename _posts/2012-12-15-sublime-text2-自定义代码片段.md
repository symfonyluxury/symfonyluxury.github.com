---
layout: post
title: "Sublime text2 自定义代码片段"
description: "很多时候我们需要一个快捷键（组合）来导入想要的代码，就能很方便的实现一个片段功能，这存在于很多大型IDE中。其实，sublime text2也支持哦"
category: IDE
tags: [sublime text2]
---
很多时候我们需要一个快捷键（组合）来导入想要的代码，比如导入一段html片段或者jquery ajax()，不用我们每次挨个的写。这存在于很多大型IDE中。其实，sublime text2也支持哦

首先进入`Tools->New Snippet`,模板大概如下:

	<snippet>
		<content><![CDATA[
	Hello, ${1:this} is a ${2:snippet}.
	]]></content>
		<!-- Optional: Set a tabTrigger to define how to trigger the snippet -->
		<!-- <tabTrigger>hello</tabTrigger> -->
		<!-- Optional: Set a scope to limit where the snippet will trigger -->
		<!-- <scope>source.python</scope> -->
	</snippet>

其中`[CDATA[]]`里的内容就是需要添加代码片段的位置。
例如在我的工作中经常需要用到twitter bootstrap代码，比如alert-message。每次都要手动写很麻烦，还需要记(好吧，我记忆是不好)。如果直接把代码写入snippet当中：

	<snippet>
		<content><![CDATA[
	    <div class="alert alert-">
		    <button type="button" class="close" data-dismiss="alert">&times;</button>
		    <strong>Warning!</strong> Best check yo self, you're not looking too good.
	    </div>
	]]></content>
		<tabTrigger>alert</tabTrigger>
		<description>twitter bootstrap alert</description>
	</snippet>

编辑器中输入`alert` 然后`tab`，以上代码就直接调出来了，是不是很方便呵呵。

{% include JB/setup %}
