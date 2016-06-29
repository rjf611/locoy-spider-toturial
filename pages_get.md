# 4.3 关联多页的文章采集


## 关联多页



当采集的信息不在当前默认页，而在当前默认页某一个链接的所在页时，此时就要用到多页管理了，

多页管理界面如下：

我们以内容页网址 http://kimi201406.1688.com/page/creditdetail.htm 为例，

来获取获取它的公司介绍和联系方式页面的联系方式信息。

公司介绍在网址 http://kimi201406.1688.com/page/creditdetail.htm 里获取， 而联系方式信息在网址 

http://kimi201406.1688.com/page/contactinfo.htm 里获取。所以我们需要借助多页功能来实现。

前者叫默认页地址，后者叫做多页地址。

流程：点击①创建多页，进行②多页设置，然后在数据来源③选择多页调用，最后根据多页源代码设置提取方式。

![](http://imgs.leesven.com/2016/locoyimgs/53.png)

下面重点讲解②，多页地址获取方式：

a.页面地址替换
b.源码中截取

**a.页面地址替换：**也就是默认页和多页地址有相同的地方，通过简单的替换就可以变成多页地址。

**b.源码中截取：**也就是多页的地址在默认页的页面源代码里面。

下面就上述网址来说明下这两种方式如何获取多页。



---



**a.页面地址替换**

比较默认页```“http://kimi201406.1688.com/page/creditdetail.htm”```和多页地

址：```“http://kimi201406.1688.com/page/contactinfo.htm”```之间的共同点，默认页“creditdetail.htm”替换

为“contactinfo.htm”就是我们的多页地址了。

设置如下图：

![](http://imgs.leesven.com/2016/locoyimgs/54.png)

正则表达式中 (.*) 为任意通配符。

$1,$2…$数字来按照顺序对应上面(.*)表示的部分。

若要对多页源码部分区域做限定，可在指定多页源码区域设置。

若留空则默认返回多页整个源代码。

设置好以后，点击测试查看结果。

**b.源码中截取**

可以看到默认页源码中有多页地址

![](http://imgs.leesven.com/2016/locoyimgs/55.png)

所以设置如下：

![](http://imgs.leesven.com/2016/locoyimgs/56.png)

保存即可。

最后设置数据来源和提取方式，如图：

![](http://imgs.leesven.com/2016/locoyimgs/57.png)

注：如需要多级多页，则在多页地址获取 方式：选择需要的多页即可

![](http://imgs.leesven.com/2016/locoyimgs/58.png)