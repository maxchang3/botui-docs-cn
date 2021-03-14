---
title: 指南
---

# 指南


## Hello World

一个使用BotUI显示 `Hello Word` 消息的基本例子。


```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>BotUI - Hello World</title>
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/botui/build/botui.min.css" />
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/botui/build/botui-theme-default.css" />
  </head>
  <body>
    <div class="botui-app-container" id="hello-world">
      <bot-ui></bot-ui>
    </div>
    <script src="https://cdn.jsdelivr.net/vue/latest/vue.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/botui/build/botui.js"></script>
    <script>
      var botui = new BotUI('hello-world');

      botui.message.add({
        content: 'Hello World from bot!'
      }).then(function () { // 等待上一条消息显示

        botui.message.add({
          delay: 1000,
          human: true,
          content: 'Hello World from human!'
        });
      });
    </script>
  </body>
</html>
```


## Messages(消息)

消息意味着要向用户展示内容。 内容简单来说可以是文本或者一些第三方的嵌入/交互服务。文本信息也可以包含超链、图像和图标。更多详情请见 [BotUI Markup](#BotUI-Markup)。

在一个BotUI实例中，使用 `message.add` 方法显示消息。
```javascript
botui.message.add({
  content: 'Hello, this is a message.'
});
```

在消息中使用html代码：

```javascript
botui.message.add({
  type: 'html', // 默认类型为`text`
  content: 'Hello, this is a <b>bold message</b>.'
});
```

在消息中嵌入youtube视频：

```javascript
botui.message.add({
  type: 'embed', // 默认类型为`text`
  content: 'https://www.youtube.com/embed/ZRBH5vHhm4c'
});
```

这样做的本质是创建一个 `iframe` 元素设置 `content` 为其 `src` 的url。因此任何在 `iframe` 中能被显示的东西都在嵌入到 `BotUI` 消息中。

你也可以显示一个“加载”状态(在UI中，由3个动画点表示)。

下面是显示“加载”消息的方法：

```javascript
botui.message.add({
  loading: true
}).then(function (index) {
  // do some stuff like ajax, etc.

  botui.message.update(index, {
    loading: false,
    content: 'Hello, this is a message.'
  });
});
```
`loding` 可以结合 `delay`(延迟)来展示“加载”用于特殊用途，然后显示原始的信息。

```javascript
botui.message.add({
  delay: 3000,
  loading: true,
  content: 'Hello, this is delayed message shown after a loading message.'
});
```

上述代码显示3秒“加载”消息会然后显示其内容。

## Action(动作)

显示一个表单来获取**文本**输入：
```javascript
botui.action.text({
  action: {
    placeholder: 'Enter your text here'
  }
}).then(function (res) { // 提交文本后回调
  console.log(res.value); // 打印提交的值 
});
```

显示一个按钮

```javascript
botui.action.button({
  action: [
    { // 只显示一个按钮
      text: 'One',
      value: 'one'
    }
  ]
}).then(function (res) { // 点击按钮会回调
  console.log(res.value); // 打印对应按钮的value
});
```

显示下拉列表

```javascript
botui.action.select({
  action: {
      placeholder : "Select Language", 
      value: 'TR', // 选定值或者对象，例如：{value: "TR", text : "Türkçe" }
      searchselect : true, // 搜索选择，默认为true，false为标准的下拉列表。
      label : 'text', // 下拉标签的值
      options : [
                      {value: "EN", text : "English" },
                      {value: "ES", text : "Español" },
                      {value: "TR", text : "Türkçe" },
                      {value: "DE", text : "Deutsch" },
                      {value: "FR", text : "Français" },
                      {value: "IT", text : "Italiano" },
                ],
      button: {
        icon: 'check',
        label: 'OK'
      }
    }
}).then(function (res) { // 按钮提交后回调
  console.log(res.value); // 打印“one”的“value”
});
```

显示多选下拉列表

```javascript
botui.action.select({
  action: {
      placeholder : "Select Language", 
      value: 'TR,EN', // 选定值或选定数组对象。 例如： [{value: "TR", text : "Türkçe" },{value: "EN", text : "English" }]
      multipleselect : true, // 默认为false
      options : [
                      {value: "EN", text : "English" },
                      {value: "ES", text : "Español" },
                      {value: "TR", text : "Türkçe" },
                      {value: "DE", text : "Deutsch" },
                      {value: "FR", text : "Français" },
                      {value: "IT", text : "Italiano" },
                ],
      button: {
        icon: 'check',
        label: 'OK'
      }
    }
}).then(function (res) { // 按钮点击后回调
  console.log(res.value); // 打印“one”的“value”
});
```

## `sub_type`(子标签)

我们可以使用`sub_type`来向用户请求不同类型的值。
例如我们请求个邮件；

```javascript
botui.action.text({
  action: {
    sub_type: 'email',
    placeholder: 'Enter your text here'
  }
});
```

这一过程的本质是设置`input`元素的`type`类型。这上述情景下，会类似于 `<input type="email" />`。

因此你可以参考<a href="https://developer.mozilla.org/en/docs/Web/HTML/Element/input#Form_%3Cinput%3E_types" target="blank">`input type`</a> . 😲


## `autoHide` (自动隐藏)

Actions are hidden as soon as they are performed. If you'd like to keep showing actions then you can set 'autoHide' to `false`.
动作(按钮或输入框)在执行后会被隐藏掉。如果你向保持显示动作你需要设置'autoHide' 为 `false`。

```javascript
botui.action.button({
  autoHide: false,//开启自动隐藏
  action: [
    {
      text: 'One',
      value: 'one'
    }
  ]
}).then(function (res) { // will be called when a button is clicked.
  botui.action.hide(); // 手动隐藏按钮.
});
```

##  `addMessage` (添加消息)

When an action is performed by user, a message from `human` side is added automatically with `action`'s data in it.

If you'd like to show a message, upon action, yourself or don't anything at all then you can control this by setting `addMessage` to `false`.

```javascript
botui.action.text({
  addMessage: false,
  action: {
    placeholder: 'Your name'
  }
}).then(function (res) { // will be called when a button is clicked.
  botui.message.add({
    human: true, // show it as right aligned to UI
    content: 'My name is ' + res.value
  });
});
```

## BotUI Markup

BotUI 支持在`message`对象的`content`中使用BotUI Markup语法。

>BotUI Markup是markdown的一个子集，也有部分内容的补充。

当前支持的部分为:

- 链接 - 使用``[内容](URL)`` 语法来显示链接
- 图像 - 使用``![替换文本](图像地址)``来显示图片
- 图标(非markdown原生) - 使用``!(图标名称)``来显示图标。


**链接**:

```javascript
botui.message.add({
  content: 'Go ahead, try [our product](https://example.com)'
});
```

会显示如下的内容：

> Go ahead, try [our product](https://example.com)

BotU 默认会在同一选项卡中打开消息中的链接，如果要在新选项卡中打开链接，只需在URL语法的末尾添加`^`。例如：

```javascript
botui.message.add({
  content: 'Go ahead, try [our product](https://example.com)^'
});
```

**图像**:

```javascript
botui.message.add({
  content: 'Here is an image ![product image](images/logo.png)'
});
```


预览:

> Here is an image ![product image](images/logo.png)

带链接的图像

```javascript
botui.message.add({
  content: 'Here is an image [![product image](images/logo.png)](https://baidu.com)'
});
```

预览:
> Here is an image [![product image](images/logo.png)](https://baidu.com)


**图标** :


如果你知道 FontAwesome，你应该很清楚知道如何显示一个对号图标，即： `<i class="fa fa-check"><i>`

同样的，在BotUI中的图标显示也使用了Font Awesome，你只需要：


```javascript
botui.message.add({
  content: '!(check) All Done!'
});
```

预览；

> <div><i class="fa fa-check"><i> All Done! </div>


## Icon (图标)

上面已经说了，BotUI 使用 FontAwesome 来显示图标。 这意味着你可以在你的消息或按钮中使用所有 FontAwesome 的图标。

只需要在`按钮`或`动作`对象中的`icon`属性中填写图标名称即可。

如下所示，在按钮中显示一个对勾图标，我们需要这样写：
```javascript
botui.action.button({
  action: [
    {
      icon: 'check',
      text: 'Continue',
      value: 'continue'
    }
  ]
})
```


## `cssClass` (css类)

由于你并不能控制UI的HTML，所以你将无法添加或删除元素。但是BotUI可以选择将CSS类应用于某些元素，然后根据需要将样式应用于它们。

`cssClass`选项支持消息、动作、输入框和按钮元素。

例如在我们的消息中应用一个自定义类：
```javascript
botui.message.add({
  cssClass: 'custom-class',
  content: '!(check) All Done!'
});
```

然后你可以在你的样式表中使用`custom-class`来应用你需要的样式。

你可以使用`cssClass`添加单个类或者使用`cssClass: ['one', 'two']`来添加一组类。

## Message `index` (索引)

将消息添加到UI时，会从内部消息数组返回该消息的“索引”。

你可以将“index”视为消息的id，但它可以更改，因此不能认为它是唯一的。

你可以使用这个`index`通过回调BotUI实例的 [`message.update`](reference.md#botui.message.update) 或 [`message.remove`](reference.md#botui.message.remove) 方法来更改或删除一个消息。

更新一个消息的内容我们可以这样做：

```javascript
botui.message.add({
  content: 'Tracking your package ...'
}).then(function (index) { // 被添加消息的`index
  //do sth here……

  //更新上一条消息

  //调用'update'方法并传递从Promise得到的'index'。

 botui.message.update(index, {
   content: 'Here is the location..'
 });

});
```
