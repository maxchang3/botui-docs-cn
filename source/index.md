---
title: 简介
---

# 关于
本文档由 [张麦麦](https://zhangmaimai.com) 汉化，若发现任何问题欢迎反馈。<a href="https://www.netlify.com/" rel="external nofollow noreferrer" class="footer-link" target="_blank"><img src="https://www.netlify.com/img/global/badges/netlify-dark.svg" style="margin-bottom:-14px"></a>
<div class="github-card" data-github="MaxChang3/botui-docs-cn" data-width="400" data-height="" data-theme="default"></div>
<script src="//cdn.jsdelivr.net/github-cards/latest/widget.js"></script>

# BotUI

> 一个用于构建Bot（机器人）UI（用户界面）的Javascript框架。

BotUI 使得创建一个会话/Bot接口变的超级简单。他提供一个直观的Javascript API来显示添加消息和可执行操作。你所看见的一切都可以通过创建 [主题](theme.html) 进行修改。


### 快速上手

看看怎么用吧。

#### HTML

在你想显示Bot的地方添加 `<bot-ui>` 标签。

```html
...

<div id="my-botui-app">
  <bot-ui></bo-tui>
</div>

...
```


#### JavaScript

将父元素的`id`传递给`BotUI`的构建函数。

```javascript
var botui = new BotUI('my-botui-app');
```

使用 `message.add` 方法来显示消息。

```javascript
botui.message.add({
  content: 'Hello There!'
}).then(function () {  // 等待上一条消息显示
  botui.message.add({ // 显示下一条消息
    content: 'How are you?'
  });
});
```

#### 总结
```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>BotUI</title>
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
    <link rel="stylesheet" href="https://unpkg.com/botui/build/botui.min.css" />
    <link rel="stylesheet" href="https://unpkg.com/botui/build/botui-theme-default.css" />
</head>

<body>
    <div id="my-botui-app">
        <bot-ui></bot-ui>
    </div>
    <script src="https://cdn.jsdelivr.net/vue/latest/vue.min.js"></script>
    <script src="https://unpkg.com/botui/build/botui.min.js"></script>
    <script>
        var botui = new BotUI('my-botui-app');
        botui.message.add({
            content: 'Hello There!'
        }).then(function () { // 等待上一条消息显示
            botui.message.add({ // 显示下一条消息
                content: 'How are you?'
            });
        });
    </script>
</body>

</html>
```
跟随后续的文档获得更详细的说明。