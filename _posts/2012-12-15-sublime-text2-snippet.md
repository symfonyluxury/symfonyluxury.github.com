---
layout: post
title: "Sublime text2 自定义代码片段"
description: "很多时候我们需要一个快捷键（组合）来导入想要的代码，就能很方便的实现一个片段功能，这存在于很多大型IDE中。其实，sublime text2也支持哦"
category: 
tags: [sublime text2]
---
首先依次进入`Tools->New Snippet`,模板大概如下:

<script src="https://gist.github.com/4295702.js"></script>
<script src="https://gist.github.com/4295941.js"></script>
其中`[CDATA[]]`里的内容就是需要添加代码片段的位置处。
在我工作过程中经常需要用到twitter bootstrap代码，比如alert-message。每次都要手动写很麻烦，还需要记(好吧，我记忆是不好)。如果直接把代码写入snippet当中：

{% include JB/setup %}
