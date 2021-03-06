```
最近更新： 2020-11-27
适用版本： 2.7.8
```

## 通知方式

- feed rss 订阅
- ifttt webhook

### Feed rss 订阅

地址为网页端口（默认为 80） + /feed
例如：**http://127.0.0.1/feed**

然后使用 rss 阅读软件直接订阅即可。

*局域网内的 RSS 只能在局域网内查看，有外网地址才能实现远程订阅*

### ifttt webhook

![](https://raw.githubusercontent.com/elecV2/elecV2P-dei/master/docs/res/iftttnotify.png)

1. 在手机上下载 ifttt 软件，注册登录，用于接收实时通知。
2. 在 ifttt 中搜索 webhook，或访问 https://ifttt.com/maker_webhooks/ ，添加 webhook 服务
3. 在 ifttt 中新建一条规则，if **Webhook** than **Notifications**。 webhook 的 Event Name（事件名称）设置为: **elecV2P**

![](https://raw.githubusercontent.com/elecV2/elecV2P-dei/master/docs/res/setiftttm.jpg)

4. 在 ifttt 的 webhook setting edit 中找到对应的 **key**, 然后把 key 填写到 webUI 后台管理页面的 setting 对应位置

![](https://raw.githubusercontent.com/elecV2/elecV2P-dei/master/docs/res/setifttt.png)

#### 测试设置是否成功

在 JSMANAGE 页面的 JS 编辑框中复制以下代码：

``` JS
$feed.ifttt('elecV2P notification', '这是一条来自 elecV2P 的通知', 'http://192.168.1.101')
```

然后点击测试运行（快捷键 ctrl+enter），如果在手机上马上收到 ifttt 的通知，表示设置成功。如果没有收到，看程序的运行日志，对照上面的步骤检查一遍。

## 默认通知内容

- 任务开始/暂停/删除/及结束
- JS 运行设定次数（默认 50）

## JS 调用 - 自定义通知

### 关键字： $feed

- $feed.push(title, description, url)     // 表示添加一个 rss item

``` JS example
$feed.push('elecV2P notification', '这是一条来自 elecV2P 的通知', 'https://github.com/elecV2/elecV2P')
```

- $feed.ifttt(title, description, url)   // 发送一条 ifttt 通知

*先设置好 ifttt webhook key*

*url 可省略*

### 其他说明

- 当通知主题（title）中含有 **test** 关键字时，自动跳过，不添加通知内容。（方便调试）
- 默认已打开 JS $notify/$notification 对应的 IFTTT 通知（version>2.6.6）