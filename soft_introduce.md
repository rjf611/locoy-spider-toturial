# 1.1 软件简介

火车采集器V9程序目录

![](http://imgs.leesven.com/2016/locoyimgs/1.jpg)
```
|-Configuration 用户配置保存目录
|-Synonym  用户同义词保存目录
|-CategoryDirweb 模块网站栏目
 --LoginConfig.ini 登陆用户账号信息
 --config.db3   任务规则配置文件
|-Data  采集数据保存目录
   |-1、2、3等   任务采集数据存储目录
|-PageUrl   任务采集网址存储目录
|-Module   Web发布模块及数据库发布模块目录
|-Plugins   c#和PHP插件存储目录
|-System  系统文件目录
   |-Logs 程序错误日志
 --LocoySpider.exe   火车采集器启动文件
 --CodeEditor.exe 源码编辑器
 --DatabaseManager.exe  数据库发布配置管理工具
 --HttpPostGet.exeHTTP 请求测试工具
 --LocoyProxy.exe  二级代理程序
 --WebPostManager.exeWeb 发布配置管理工具
 --uninst.exe   卸载程序 
 --UpdateToV9.exe V7,V8升级到V9程序
 ```