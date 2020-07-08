# 微信直播开发小程序live-pusher/live-player使用示例

本仓库包括的内容
* 使用开源组件搭建本地的RTMP服务给小程序使用
* 小程序live-pusher/live-player如何使用
* 使用网页播放小程序推的视频流
* 关于腾讯云实时流媒体服务

## 本栗子使用流程图
<img src="./assets/liu-chen-tu.jpg"/>

## 文件夹说明
* assets - 截图目录
* client - 微信小程序源代码, 微信开发者工具打开这个文件夹
* Node-Media-Server - 本地的RTMP服务 (支持RTMP,FLV)
* web-client - 网页访问本地的RTMP服务, 在网页播放RTMP推送的视频流(flv格式播放)


## 开源组件搭建本地的RTMP服务
命令行进入文件夹 Node-Media-Server, 执行
```text
npm install
node index.js
```

程序默认将在1935端口提供RTMP服务, 8000端口提供HTTP流服务

程序使用第三方开源MIT协议组件 Node-Media-Server 


## 小程序live-pusher/live-player如何使用
<b>开始之前你需要在微信开放平台注册小程序开发账号, 并申请小程序接口实时音视频流权限</b>
这一步很重要, 不完成这一步无法进行后面的开发. 

个人账号是可以申请此类接口权限的.

当小程序账号注册完成以及申请实时音视频流权限之后.\
获取appid\
并使用微信开发者工具导入项目, 选择 client 文件夹, 
然后点击 `真机调试`, 使用手机微信调试RTMP视频流.
<b>记住要先开启本地的RTMP服务哦</b>, 至于IP地址配置会在小程序页面有提示的.



## 使用网页播放小程序推的视频流
前面两步都完成的情况下, 可以在网页上测试一下小程序推的视频流.
命令行进入 `web-client` 文件夹, 然后命令行执行如下命令 :
```text
// 如果你的npm已经全局安装了http-server
http-server -p 8080

// 否则
npm install
npx http-server -p 8080
```
然后浏览器打开 [http://localhost:8080](http://localhost:8080),
根据网页的提示填写拉取流的名称, 然后点击`开始`按钮, 如果不出意外你可以看到小程序推上来的视频流.

网页测试截图 \
<image src="assets/网页测试截图.jpg" width='300' />

## 关于腾讯云实时流媒体服务
有些同学如果关心腾讯云实时流媒体服务怎么用的话, 可以进入腾讯云申请相应服务即可, 腾讯云有免费的20GB流量
供大家测试使用. 

至于具体的使用方法与上面的例子是一样的, 从腾讯云网页获取推流/拉流的地址就可以测试了.

如果你深入测试会发现腾讯云的速度比较快, 那是因为. \
腾讯云的RTMP服务是私有的 UDP + RTMP 协议, 传输层使用UDP协议在实时视频中可以将延时控制在 400ms左右.

而我们自己搭建的RTMP服务是基于 TCP 传输的, 我在测试过程中发现宽带情况, 好的4G, 5G下, 基于TCP传输协议的实时视频的延时大概在1秒钟左右.
但是对于WIFI等网络波动大的情况下大概会有2秒的延时

那你就想问, 我们把自己的RTMP服务改成UDP传输不好吗?\
很抱歉, 截止 2019年3月5日 (我会持续关注腾讯并更新) \
在微信小程序环境 \
只有 \
腾讯云自家的RTMP服务 \
才能使用UDP传输层协议 \

目前我测试了微信小程序环境, 其它家的产品:
* 声网(agora) 实时视频  基于TCP传输
* 阿里云 - 没有相应服务
* 百度云 - 没有相应服务

数据真实可靠, 都是我测试或者从他们工程师那里询问得知的.

但其实使用TCP的实时视频服务没那么糟糕, 在好的4G情况下 \
1秒钟的延时用户完全是可以接受的 \
当然如果老板没办法接受, 那就使用腾讯云了呗. \
本人亲测, 小鱼易联/小鱼在家 产品使用的就是腾讯云的服务.

<b>以上所述都是截止于 2019年3月5日 , 后面微信小程序的策略发生变动我会第一时间更新, 逃~~~</b>

## 链接
* [Node-Media-Server](https://github.com/illuspas/Node-Media-Server)
* [腾讯云直播服务, 免费20GB流量](https://console.cloud.tencent.com/live)


## 一些配置截图
<image src="assets/小程序接口设置.jpg" />
<image src="assets/wifi-ip地址.jpg" />
