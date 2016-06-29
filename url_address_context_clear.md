# 采集页地址，内容过滤和插件说明

**采集页地址**

采集默认页或者多页等页地址。通过设置数据来源来选择默认页或多页。
提取方式：正则提取，```^(?<content>[\s\S]*?)$```

![](http://imgs.leesven.com/2016/locoyimgs/59.png)

**内容过滤**


有时有些采集的数据不需要怎么办？火车采集器的内容过滤功能可以完成这个工作。

第二步：采集内容规则---数据处理---内容过滤

内容过滤有以下几个处理方法： 

* 1.内容不得包含和内容必须包含：
  可以设置多个词，支持选择 a.所有条件都必须满足  或 b.满足其中一个条件即可
* 2.采集结果不得为空：该功能可以让某个字段不出现空内容。
* 3.采集结果不得重复：该功能可以让某个字段不出现重复内容。设置此项前请确保您没有采集过数据，或者请先清空采集数据。
* 4.当内容长度小于(大于，等于，不等于)N时过滤：一个符号或一个字母或一个数字或一个汉字都算一个。

![](http://imgs.leesven.com/2016/locoyimgs/134.png)

不符合要求的数据将被删除。


**HTTP请求插件**

可以修改HTTP请求前的请求数据（http header）和HTTP完成后的返回数据（response），这个插件包含了2个处理方法。

```BeforeRequest(RequestEntry request)```

这个方法会在所有HTTP请求前的调用，包括网址采集、内容采集请求，可以通过修改请求来应对一些复杂的网站抓取。

参数介绍：

request 参数中包含Url、Referer、Cookie、Headers、页面类型等,除HTTP基本属性外，还有包含一些特殊值

request.Properties["PageType"]， 这个属性是页面类型，值为整数类型，包含6种类型

0：起始地址； 1：列表页面； 2：列表页的分页； 3：内容页面； 4：关联多页； 5：内容页的分页；

request.Properties["JobName"]，任务名称

request.Properties["JobID"]，任务ID

request.Properties 属性最好只做读取操作，不要修改，不然会造成无法预料的结果。其他的RequestEntry字段请参考 [文章最后]

```AfterResponse(ResponseEntry response)```

这个方法在所有HTTP请求完成后调用，可以修改为自己想要的数据，然后交给采集器来处理。

参数介绍：

response中包含HTTP响应数据，如返回HTML、响应Header

response.RawText`，是返回的HTML代码

response.Url`，请求的Url地址和 request 一样，response 也包含了 response.Properties["PageType"]、request.Properties["JobName"]、request.Properties["JobID"]，含义相同。

其他的ResponseEntry字段请参考 [文章最后]

示例插件代码：

```
public class Plugin1 : IHTTPTamper
{
    /// <summary>
    /// 处理下载前的request
    /// </summary>
    /// <param name="response"></param>
    public void BeforeRequest(RequestEntry request) {
        Console.WriteLine("BeforeRequest："+request.Url);
    }
    /// <summary>
    /// 处理下载完成后的http响应,网址、默认页、多页、内容分页
    /// </summary>
    /// <param name="response"></param>
    public void AfterResponse(ResponseEntry response) {
        Console.WriteLine("AfterResponse：" + response.Url);
    }
}
```

**内容数据插件**

通过这个插件可以修改最终的标签数据结果。

内容插件处理方法 ```Process(ResponseEntry response, Dictionary<string, string> result)```

参数介绍：

response，内容页的响应结果
result，是标签数据结果，键是标签名称，值是标签数据。
可以修改result中的值，但是不要删除、清空 result 的键，不然保存数据时可能会出错。

示例插件代码：

```
public class Plugin2 : IResultProcesser
{
    /// <summary>
    /// 处理采集后的标签结果
    /// </summary>
    /// <param name="response">默认页面的响应</param>
    /// <param name="result">标签结果，键为标签名称，值为标签值</param>
    public void Process(ResponseEntry response, Dictionary<string, string> result)
    {
        Console.WriteLine("Process：" + response.Url);
        var m = Regex.Match(response.RawText, "<title>(?<t>[^<]*)");
        if (m.Success)
        {
            Console.WriteLine(response.Url);
        }
    }
}
```

**文件下载插件**

这个插件提供下载文件的相关信息，并且修改其中的某些值。

处理方法：```BeforeDownload(RequestEntry request, DownloadFile downloadFile)```

参数介绍：

request 是文件下载HTTP的请求数据，详细参考 [文章最后]RequestEntry

downloadFile，文件下载的相关属性，包括下载地址、保存路径、HTML中的替换路径等等

示例插件代码：

```
public class Plugin3 : IFileDownloader
{
    /// <summary>
    /// 文件下载前的处理方法
    /// </summary>
    /// <param name="request">文件下载的HTTP请求</param>
    /// <param name="downloadFile">下载文件</param>
    public void BeforeDownload(RequestEntry request, DownloadFile downloadFile)
    {
        if (downloadFile.DownlaodUrl.Contains("xxx"))
        {
            downloadFile.Cancel = true;//取消该文件的下载
        }
    }
}
```
RequestEntry 详细字段说明

```
public class RequestEntry
{
        /// <summary>
        /// 请求的头信息
        /// </summary>
        public Dictionary<string, string> Headers { get; set; }
        /// <summary>
        /// HTTP请求的方式，GET或者POST
        /// </summary>
        public string Method { get; set; }
        /// <summary>
        /// 请求的地址
        /// </summary>
        public string Url { get; set; }
        /// <summary>
        /// 来源地址
        /// </summary>
        public string Referer { get; set; }
        /// <summary>
        /// POST数据，当Method为POST时生效
        /// </summary>
        public string PostData { get; set; }
    /// <summary>
    /// 请求编码
    /// </summary>
        public string Encoding { get; set; }
}
```

ResponseEntry 详细字段说明

```
public class ResponseEntry
{   
    /// <summary>
    /// 页面编码,比如UTF-8,GB2312
    /// </summary>
    public string ContentEncoding { get; set; }
    /// <summary>
    /// 页面类型,比如text/plain,text/html,application/xml
    /// </summary>
    public string ContentType { get; set; }
    /// <summary>
    /// 响应的HTTP头信息
    /// </summary>
    public Dictionary<string, string> Headers { get; set; }
    /// <summary>
    /// POST或者GET
    /// </summary>
    public string Method { get; set; }
    /// <summary>
    /// 来源页地址
    /// </summary>
    public string Referer { get; set; }
    /// <summary>
    /// 响应地址
    /// </summary>
    public Uri ResponseUri { get; set; }
    /// <summary>
    /// HTTP状态代码
    /// </summary>
    public HttpStatusCode StatusCode { get; set; }
    /// <summary>
    /// 请求地址
    /// </summary>
    public string Url { get; set; }
    /// <summary>
    /// HTTP响应中的原始文本
    /// </summary>
    public string RawText { get; set; }
}
```

DownloadFile 详细字段说明

```
public class DownloadFile
{
    /// <summary>
    /// 所属的记录ID
    /// </summary>
    public int ContentId { get; set; }
    /// <summary>
    /// 原始下载地址
    /// </summary>
    public string DownlaodUrl { get; set; }
    /// <summary>
    /// 最终下载地址
    /// </summary>
    public string FinalDownloadUrl { get; set; }
    /// <summary>
    /// 文件保存路径
    /// </summary>
    public string FileName { get; set; }
    /// <summary>
    /// html中的替换路径
    /// </summary>
    public string ReplaceUrl { get; set; }
    /// <summary>
    /// 标签名称
    /// </summary>
    public string LabelName { get;set; }
    /// <summary>
    /// 所属的页面地址
    /// </summary>
    public string PageUrl { get;set; }
    /// <summary>
    /// 是否取消下载
    /// </summary>
    public bool Cancel = false;
}
```