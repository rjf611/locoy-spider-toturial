# 7.1 一个简单的文章规则制作

一个简单的文章规则制作

通过采集faq为例来说明采集器采集的原理和过程。

本例以 http://faq.locoy.com/qc-12.html 演示地址。

**（1）新建个采集规则**

选择一个分组上右击，选择“新建任务”，如下图：

![](http://imgs.leesven.com/2016/locoyimgs/106.png)

（2）添加起始网址
在这里我需要采集 5页数据。

分析网址变量规律

第一页地址：http://faq.locoy.com/qc-12.html?p=1

第二页地址：http://faq.locoy.com/qc-12.html?p=2

第三页地址：http://faq.locoy.com/qc-12.html?p=3

由此我们可以推算出p=后的数字就是分页的意思，我们用[地址参数]表示：

所以设置如下:

![](http://imgs.leesven.com/2016/locoyimgs/107.png)

地址格式：把变化的分页数字用[地址参数]表示。

数字变化：从1开始，即第一页；每次递增1，即每次分页的变化规律数字； 共5项，即一共采集5页。

预览：采集器会按照上面设置的生成一部分网址，让你来判读添加的是否正确。

然后确定即可

**（3）[常规模式]获取内容网址**

常规模式：该模式默认抓取一级地址，即从起始页源代码中获取到内容页A链接。

在这里给大家演示用 自动获取地址链接 +设置区域 的 方式来获取。

查看页面源代码找到文章地址所在的区域：

![](http://imgs.leesven.com/2016/locoyimgs/108.png)

设置如下：

注：更详细的分析说明可以参考本手册：

![](http://imgs.leesven.com/2016/locoyimgs/109.png)

操作指南 > 软件操作 > 网址采集规则 > 获取内容网址

点击网址采集测试，看看测试效果

![](http://imgs.leesven.com/2016/locoyimgs/110.png)

（3）内容采集网址

以 http://faq.locoy.com/q-1184.html 为例讲解标签采集

注：更详细的分析说明可以参考本手册

操作指南 > 软件操作 > 内容采集规则 > 标签编辑

我们首先查看它的页面源代码，找到我们“标题”所在位置的代码：

```<title>导入Excle是跳出对话框~打开Excle出错 - 火车采集器帮助中心</title>```

分析得出： 开头字符串为：```<title>```

结尾字符串为：```</title>```

数据处理——内容替换/排除：需要把- 火车采集器帮助中心 给替换为空

![](http://imgs.leesven.com/2016/locoyimgs/112.png)

内容标签的设置原理也是类似的，找到内容所在源码中的位置

![](http://imgs.leesven.com/2016/locoyimgs/111.png)

分析得出： 开头字符串为：```<div id="cmsContent">```

结尾字符串为：```</div>```

数据处理——HTML标签排除：把不需要的A链接等 过滤

![](http://imgs.leesven.com/2016/locoyimgs/113.png)

再设置个“来源”字段

![](http://imgs.leesven.com/2016/locoyimgs/114.png)

这样一个简单的文章采集规则就做好了。