# 2.1 开始菜单


![](http://imgs.leesven.com/2016/locoyimgs/3.png)
**1.新建分组**

新建一个任务分组，选择所属分组，确定分组名称和备注。

**2.新建任务**

确定所属分组，新建一个任务，填写任务名称并保存。

**3.Web发布配置**

Web发布配置定义了如何登陆一个网站以及向该网站提交数据。

主要涉及到登录信息的获取，网站编码设定，栏目列表的获取，以及使用数据测试发布效果。 

详细教程后续讲解。

![](http://imgs.leesven.com/2016/locoyimgs/4.png)

**4.Web发布模块**

可以定义网站登录，获取栏目列表，获取网页随机值，内容发布参数，以及上传文件，构造发布数据等高级功能。

详细教程后续讲解。

**5.数据库发布配置**

数据库发布配置定义了数据库链接信息的设置以及数据库模块的选择。

详细教程后续讲解。

**6.数据库发布模块**

用于编辑数据库的发布模块，方便我们将数据发布到配置好的数据库中。

火车采集器可选mysql、sqlserver、oracle、access四种数据库类型，在文本输入框中填写sql语句（需有数据库相关知识），并可使用标签替换相应数据。也可在采集器模块文件夹中加载某一模块进行编辑。

详细教程后续讲解。

![](http://imgs.leesven.com/2016/locoyimgs/6.png)

**7.计划任务**

设置列表中采集任务的启动计划，可每间隔、每天、每周、仅一次、或自定义Cron表达式，

（Cron表达式的写法可参考相关术语中的介绍）。保存设置后，任务即可按照设置执行。

详细教程后续讲解。

![](http://imgs.leesven.com/2016/locoyimgs/7.png)

**8.插件管理**

插件是可以用来扩展火车采集器功能的程序

火车采集器V9支持PHP源码、C#源码、C#类库三种类型的插件，

可用于扩展http请求、内容处理和文件下载的功能，并可以分别进行测试。

详细教程后续讲解。

**9.http二级代理**

网络中的代理服务器，可以代理网络用户去取得所需要的网络信息。

代理的功能有可以突破自身ip的访问限制访问国外站点，访问一些单位或团体内部资源，

突破电信的ip封锁和隐藏真实的ip等。

火车采集器V9支持http代理、socket4和socket5代理。

详细教程后续讲解。

![](http://imgs.leesven.com/2016/locoyimgs/8.png)

**10.http模拟请求**

可以设置如何发起一个http请求，包括设置请求信息，返回头信息。并具有自动提交的功能。

详细教程后续讲解。