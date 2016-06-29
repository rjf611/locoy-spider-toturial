# 6.6 XPATH提取

**XPath提取**

 XPath 是一门在 HTML/XML 文档中查找信息的语言。
 
 XPath 使用路径表达式在 XML 文档中进行导航,可以通过FireFox firebug 或者Chrome 开发者工具快速获取。

**XPath节点属性**

 ```
 innerHTML 获取位于对象起始和结束标签内的 HTML (HTML代码，不包含开始/结束代码)
 innerText 获取位于对象起始和结束标签内的文本 (文本字段，不包含开始/结束代码)
 outerHTML 获取对象及其内容的 HTML 形式 (HTML代码，包含开始/结束代码)
 Href      获取超链接 
 ```

以网址 http://faq.locoy.com/q-681.html 为例，我们来设置标题和内容的XPath表达式，节点属性 我们默认innerHTML就可以。

**方法/步骤**

1、首先，用谷歌浏览器打开 网页， 然后打开Chrome开发者工具，快捷键为 “ F12 ”，反复按下F12可以切换状态（打开或关闭）。 当然，你也可以在原网页，直接右击“审查元素”。

2、获取标题的XPath，操作如下图：

![](http://imgs.leesven.com/2016/locoyimgs/143.png)

得出代码为 ```//*[@id="mainContent"]/div[2]/h2```

![](http://imgs.leesven.com/2016/locoyimgs/144.png)

3、获取内容的XPath，操作如下图：

![](http://imgs.leesven.com/2016/locoyimgs/145.png)

得出代码为 ```//*[@id="cmsContent"]```

然后放入即可。