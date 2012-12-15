---
layout: post
title: "Sublime text2 自定义代码片段"
description: "很多时候我们需要一个快捷键（组合）来导入想要的代码，就能很方便的实现一个片段功能，这存在于很多大型IDE中。其实，sublime text2也支持哦"
category: 
tags: [sublime text2]
---
首先依次进入`Tools->New Snippet`,模板大概如下:

<pre class="prettyprint linenums">
<snippet>
	<content><![CDATA[
Hello, ${1:this} is a ${2:snippet}.
]]></content>
	<!-- Optional: Set a tabTrigger to define how to trigger the snippet -->
	<!-- <tabTrigger>hello</tabTrigger> -->
	<!-- Optional: Set a scope to limit where the snippet will trigger -->
	<!-- <scope>source.python</scope> -->
</snippet>
</pre>

其中`[CDATA[]]`里的内容就是需要添加代码片段的位置处。
在我工作过程中经常需要用到twitter bootstrap代码，比如alert-message。每次都要手动写很麻烦，还需要记(好吧，我记忆是不好)。如果直接把代码写入snippet当中：

<pre class="prettyprint linenums">
<pre class="prettyprint linenums">
    <!-- 包围其中 -->
</pre>
</pre>

{% include JB/setup %}
