# 6.7 Json提取

**JSON提取**

```
JSON  结构有两种结构 
json简单说就是javascript中的对象和数组，所以这两种结构就是对象和数组两种结构，通过这两种结构可以表示各种复杂的结构

1、对象：对象在js中表示为“{}”括起来的内容，数据结构为 {key：value,key：value,...}的键值对的结构，在面向对象的语言中，key为对象的属性，
value为属性值，
所以很容易理解，取值方法为 对象.key 获取属性值，这个属性值的类型可以是 数字、字符串、数组、对象几种。
2、数组：数组在js中是中括号“[]”括起来的内容，数据结构为 ["java","javascript","vb",...]，取值方式和所有语言中一样，使用索引获取，
字段值的类型可以是 数字、字符串、数组、对象几种。
```

经过对象、数组2种结构就可以组合成复杂的数据结构了。

如：

```
{ "name": "中国", "province": [{ "name": "黑龙江", "cities": { "city": ["哈尔滨", "大庆"] } }, { "name": "广东", "cities": { "city": ["广州", "深圳", "珠海"] } }, { "name": "台湾", "cities": { "city": ["台北", "高雄"] } }, { "name": "新疆", "cities": { "city": ["乌鲁木齐"] } }] }
```

我们可以借助工具http://tool.oschina.net/codeformat/json 测试是否是JSON,格式化后如图：

![](http://imgs.leesven.com/2016/locoyimgs/136.png)

下面举例说明JSON提取的2种方式：

**1、JSON数据源：URL网址：**

我们需要对JSON网址 http://car.interface.autohome.com.cn/dealer/LoadDealerPrice.ashx?_callback=LoadDealerPrice&type=1&seriesid=3170&city=340100 做采集

分析得出：此URL的整个源代码是个完整的JSON。 所以JSON数据源选择 URL网址

![](http://imgs.leesven.com/2016/locoyimgs/138.png)

然后勾选循环匹配，就可以采集到整个JSON里的数据里

如图：

![](http://imgs.leesven.com/2016/locoyimgs/139.png)

**2、JSON数据源：JSON文本： 另外一种情况，网址里的源码不全是JSON，而只是一部分代码是JSON形式，此时我们需要提取出这段JSON文本，然后再格式化。**

例如网址 http://car.autohome.com.cn/config/series/3170.html

![](http://imgs.leesven.com/2016/locoyimgs/140.png)

所以我们需要通过多页的形式，来获取本页地址里这部分JSON代码，然后在设置JSON表达式。

![](http://imgs.leesven.com/2016/locoyimgs/141.png)

如图

![](http://imgs.leesven.com/2016/locoyimgs/142.png)