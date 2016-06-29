# 3.6 列表上下分页


对于设置列表分页，下图的起始网址--批量网址设置是最常见也是最常用的。

![](http://imgs.leesven.com/2016/locoyimgs/33.png)

现在我们用另外一种获取分页的办法，即通过列表上下页无限分页采集获取功能来自动获取分页。

使用这个功能，起始页就只需要把首页地址添加进去就可以了，如下图：

![](http://imgs.leesven.com/2016/locoyimgs/34.png)

然后进入[高级模式]-分页设置，设置区域开始字符串、区域结束字符串、地址样式、分页地址等字段。

![](http://imgs.leesven.com/2016/locoyimgs/35.png)

我们以http://news.qq.com/newsgn/zhxw/shizhengxinwen.htm 为例，我们看下第一页分页源代码的情况如下：

![](http://imgs.leesven.com/2016/locoyimgs/37.png)

我们看下第二页分页源代码的情况如下：

![](http://imgs.leesven.com/2016/locoyimgs/38.png)

```分析得出：当前页都是在<div class="pageNav">后的<strong></strong>这个代码后面紧接着一个<a href="">就是下一页地址。 也就是说我们是要通过当前页获取下一页，这样一级一级的向下获取，直至把所有分页获取到。 所以，区域开始字符串为：<div class="pageNav">(*)</strong> 区域结束字符串为：</a>(*)</div>```

地址样式根据截取区域的格式来写：```<a href="[参数]">```

效果如下：

![](http://imgs.leesven.com/2016/locoyimgs/40.png)

另外上图 “4” 即采集4页的意思，默认“0”为不限，采集所有分页。