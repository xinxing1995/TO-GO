# eventDoc

这个Repo用于记录TOGO和Wangcai的Firebase事件打点。
所有事件记录在Issue中。

## Issue格式说明
标题为打点的中文解释，和事件名

Issue正文需要说明打点的触发条件，和参数设置。

正文中永远是当前最终的状态。

打点的更新和疑问请在Issue下面评论。

**这个地方的Issue是为了记录所有的事件，以及方便后续的查询，不是用来提需求的，不要随便在这里写Issue**

## Label说明：
* **TOGO** ：这个点存在于TOGO中
* **Wangcai** ： 这个点存在于Wangcai中
* **New** : 新增打点
* **Update** ： 对打点的事件参数有更新
* **\?**：对于这个打点有疑问
* **invalid**：打点已经失效

# Protocol

Key|Value  
-----|-----
Log Destination|log.funshareapp.com/v1/funshareapp/logs/
Port|80
Protocol|HTTP/1.1
Method|POST
Header|Content-Type: application/json

统计数据会分两类数据，分别以HTTP Parameter和POST DATA的方式发送给后端Server。DATA中的数据要求是json格式。
Parameter中包含字段名(带*表示为可选)：

- - - - - - - 
1. 考虑可以从业务逻辑中删除掉一些统计代码。
2. 建议不同的event类型可以使用不同的发送策略，有些低频操作直接发好些。
3. **注意要分散上报log，尤其是用户被push激活时，如果发log基本必挂。**

## 所有事件列表
自定义统计类型|类型代号
-----|-----
点击统计|click
点击触发统计|click_begin
时长统计|duration
列表新闻渲染|load
列表新闻销毁|unload
首屏点击率统计|ctr
推送到达统计|push
分享统计|share
字体大小统计|font_size
移动网络下无图模式统计| no_pic_mode
push展现形式|push_show_type
刷新延迟|refresh
全屏播放事件|landscape

- - - - - - - - 

> 客户端事件上传逻辑: 产生事件 -> 缓存到数据库 -> 上传成功 -> 删除缓存. Android客户端 lite v2.0.6 开始大规模迁移log统计方式.


## 基本参数 ( url中的参数 )

Field Name|Key Name|Description
-----|-----|-------
IP地址|ip
屏幕尺寸|size
屏幕分辨率|resolution|格式为 1280 * 720, 高度*宽度
机型|model
语言|lang|hi,en
操作系统|os
系统版本号|os_v
app版本号|app_v
渠道|channel
网络环境|net
用户类型|u_type|fb或者device
广告id*|aid| Android字段名,可能为空
设备唯一id|did
imei*|imei|iOS可能为空
mac*|mac|iOS可能为空
android_id*|android_id | Android字段名
idfa*|idfa| iOS字段名
时间戳|ts(utc时间)|1464605889(10位)
统计接口版本|lv|1,2...
应用包| app_mode | origin或者lite 
