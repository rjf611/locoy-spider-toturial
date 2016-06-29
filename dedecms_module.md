# 7.2 DEDECMS发布模块制作

**dedecms文章发布模块制作**

WEB发布模块，即采集器把你手动在网站后台发布内容的整个过程包含登录网站后台，选择栏目，以及发布文章，这些步骤写到采集器里面，模拟发布，这就是WEB发布模块。
 
然后规则采集到的值就通过标签名传递给在线发布模块，把数据提交到网站里去。

点击开始菜单--新建

![](http://imgs.leesven.com/2016/locoyimgs/115.png)


网站自动登录：设置网站登录信息的数据 获取栏目列表：设置发布的栏目列表

网页随机获取：设置post数据内的随机值

内容发布参数：设置发布页面POST数据包

高级功能：文件上传设置以及数据构造

我们以dedecms的文章发布为例做讲解

**(1)第二步骤，“WEB发布设置界面”和 “内容发布参数” 设置**

我们在发布页面填写好需要发布的字段值（先不要点击发布），然后打开fiddler(注意，如果有乱七八糟的数据流，请先Ctlr+X 清空数据流)

如图，填写标题，来源，选择栏目，内容 ：

![](http://imgs.leesven.com/2016/locoyimgs/116.png)


Ctlr+X 清空数据流后的fiddler

![](http://imgs.leesven.com/2016/locoyimgs/117.png)


此时点击发布，分析fiddler里的数据包，将fiddler点击 ①➯ ② ，依次点击数据流列表⑤ 找到POST类型的数据流⑥， 然后点击⑦ 以文本的形式查看

![](http://imgs.leesven.com/2016/locoyimgs/118.png)


数据包贴出如下：

```
POST http://127.0.0.1:801/dede/dede/article_add.php HTTP/1.1
Host: 127.0.0.1:801
Connection: keep-alive
Content-Length: 3571
Cache-Control: max-age=0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Origin: http://127.0.0.1:801
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/43.0.2357.124 Safari/537.36
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary6EWX666GAXOVqWCE
Referer: http://127.0.0.1:801/dede/dede/article_add.php?channelid=1&cid=0
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.8
Cookie: menuitems=1_1%2C2_1%2C3_1; PHPSESSID=f21a42f70199c81955f3219623343735; DedeUserID=1; DedeUserID__ckMd5=91a12e3e1eae3a4d; DedeLoginTime=1444806848; DedeLoginTime__ckMd5=65d5fa4845a7ec00; ENV_GOBACK_URL=%2Fdede%2Fdede%2Fcontent_list.php%3Fchannelid%3D1

------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="channelid"

1
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="dopost"

save
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="title"

11111
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="shorttitle"


------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="redirecturl"


------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="tags"


------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="weight"

99
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="picname"


------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="litpic"; filename=""
Content-Type: application/octet-stream


------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="source"

22222
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="writer"


------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="typeid"

2
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="typeid2"


------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="keywords"


------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="autokey"

1
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="description"


------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="dede_addonfields"


------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="remote"

1
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="autolitpic"

1
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="needwatermark"

1
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="sptype"

hand
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="spsize"

5
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="body"

222222222222222
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="voteid"


------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="notpost"

0
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="click"

137
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="sortup"

0
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="color"


------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="arcrank"

0
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="money"

0
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="pubdate"

2015-10-14 15:16:06
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="ishtml"

1
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="filename"


------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="templet"


------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="imageField.x"

37
------WebKitFormBoundary6EWX666GAXOVqWCE
Content-Disposition: form-data; name="imageField.y"

18
------WebKitFormBoundary6EWX666GAXOVqWCE--
```

**先来设置WEB发布配置界面**

根据上面的数据包得出： 网站编码是：utf-8 （可以在您的网站右击查看源代码，查找charset字段值，具体看编码）

网站地址是： ```http://127.0.0.1:801/dede``` （网站地址可以根据POST 和Referer字段自定义，一般我们用网站域名做

网站地址，也可以找其他的2个设置的共同部分做网站地址。 ）

cookie是：

```
menuitems=1_1%2C2_1%2C3_1; PHPSESSID=f21a42f70199c81955f3219623343735; DedeUserID=1; DedeUserID__ckMd5=91a12e3e1eae3a4d; DedeLoginTime=1444806848; DedeLoginTime__ckMd5=65d5fa4845a7ec00; ENV_GOBACK_URL=%2Fdede%2Fdede%2Fcontent_list.php%3Fchannelid%3D1

```

user-agent是：

```
Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/43.0.2357.124 Safari/537.36

```

![](http://imgs.leesven.com/2016/locoyimgs/119.png)


**接下来 我们在设置 “内容发布参数”**

网站地址+发布地址后缀：需要正好组合成一个完整的地址，所以不要2者的设置是相辅相成

网站地址+来源页面后缀：需要正好组合成一个完整的地址，所以不要2者的设置是相辅相成

![](http://imgs.leesven.com/2016/locoyimgs/120.png)


然后我们把发布POST数据 里的值 替换成标签。

双击选中表单值，然后鼠标悬停在 标签按钮上，对应选择要替换成的标签名即可，可选系统标签，常用标签，时间标签。

如下图我替换的效果

![](http://imgs.leesven.com/2016/locoyimgs/121.png)


标题，来源，内容，时间 很方便确认识别。

在这里给大家讲解下“[分类ID]” 系统标签。

此标签是用于接下来我们的获取栏目列表设置做铺垫的。

那么如何确定 哪个表单名 就是 [分类ID]呢？

可以按如下图的方法，就很简单的知道，typeid 就是我们要找的 [分类ID]，给对应替换即可。 

![](http://imgs.leesven.com/2016/locoyimgs/122.png)


**（2）第二步骤，确定“获取栏目列表” 设置**

首先要确定我们的选择栏目列表是在哪个页面？

A.最常见的一种，栏目选择就是在发布内容页面里，类似我们演示的DEDE文章发布。

B.特殊的情况，在其它页面下，不在发布内容页面。

在这里我们讲解A种情况，把“内容发布参数” 下的来源页面后缀的设置，拿过来直接使用即可。

放入到“获取栏目列表” 下的 发表地址后缀，和来源页面后缀中。

然后再查看发布页面的源代码，找到刷新列表部分的源码，确定栏目列表的开始和结束代码，以及格式

![](http://imgs.leesven.com/2016/locoyimgs/123.png)


ID 用[分类ID]替换 

栏目名称用 [分类名称]替换

不规则出现的代码 用 (*)通配符匹配

设置如图：

![](http://imgs.leesven.com/2016/locoyimgs/124.png)


现在我们保存发布模块，大概测试下发布效果

可以刷新列表，说明我们的“获取栏目列表” 设置没问题。

![](http://imgs.leesven.com/2016/locoyimgs/125.png)


可以发布，说明我们的 “内容发布参数” 设置没问题。

![](http://imgs.leesven.com/2016/locoyimgs/126.png)


**（3）第三步骤，完善模块**

成功，失败标识码：

可以在网站发布正常的内容，和发布失败的内容（比如不填写标题，不选择栏目）看看分别的提示，然后写入模块设置，多个提示一行一个。

![](http://imgs.leesven.com/2016/locoyimgs/127.png)


高级功能：

可以看到我们此模块有个 LITPIC 表单名 字段，这是我们在“内容发布参数” 的黏贴POST数据时，自动提取的设置。在这里，我们可以自定义修改标签名，如设置为缩略图。

文件上传设置里的标签，文件上传不需要设置FTP，只要下载到本地就可以实现自动上传操作。

![](http://imgs.leesven.com/2016/locoyimgs/128.png)


网站自动登录：

之前我们做的发布是在登录方式为内置浏览器的原理基础上获取cookie和User-agent 来做发布的。 我们也可以用数据包登录的方式来设置。 他的设置原理和“内容发布参数” 一样的，用fiddler工具抓取登录后台那一瞬间的POST数据包。

```
POST http://127.0.0.1:801/dede/dede/login.php HTTP/1.1
Host: 127.0.0.1:801
Connection: keep-alive
Content-Length: 112
Cache-Control: max-age=0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Origin: http://127.0.0.1:801
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/43.0.2357.124 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Referer: http://127.0.0.1:801/dede/dede/login.php?gotopage=%2Fdede%2Fdede%2Findex.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.8
Cookie: menuitems=1_1%2C2_1%2C3_1; PHPSESSID=f21a42f70199c81955f3219623343735; ENV_GOBACK_URL=%2Fdede%2Fdede%2Fcontent_list.php%3Fchannelid%3D1

gotopage=%2Fdede%2Fdede%2Findex.php&dopost=login&adminstyle=newdedecms&userid=admin&pwd=admin&validate=lcmt&sm1=
```

设置如下：

![](http://imgs.leesven.com/2016/locoyimgs/129.png)


测试效果：

![](http://imgs.leesven.com/2016/locoyimgs/130.png)


OK ，这样模块用 内置浏览器登录 或 数据包登录 都是支持的了。