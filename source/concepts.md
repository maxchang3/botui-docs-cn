---
title: 概念
---

# BotUI 概念

BotUI 有以下几个重要的部分：

1. Message (消息)
2. Action (动作)
3. .then() 的使用

## Message 消息

消息 是在UI中显示的文本，他可以由Bot或用户发起。

Bot的消息会左对齐显示，用户的消息会右对齐显示，并且消息框的背景与Bot的消息不同。

开发者可以完全控制要显示的消息类型和其内容。

以下是显示Bot消息的方法：

```javascript
botui.message.add({
  content: 'Hello from bot.'
});
```

以下是显示用户消息的方法：

```javascript
botui.message.add({
  human: true,
  content: 'Hello from human.'
});
```


请注意，这两个方法的唯一不同之处就是`human: true`。如果觉得这样麻烦，你也可以分别使用`message.bot`或`message.human`来代替`message.add`。他们分别的作用是很直观的。

## Action 动作

动作可以是一个`输入框`或者是一组`按钮`。

开发者可以显示或隐藏动作。但是一次只能显示一种类型的动作。

以下显示如何询问用户的姓名：

```javascript 
botui.message.add({ // 显示一条消息
  human: true,
  content: 'Whats your name?'
}).then(function () { // 等待上一条消息显示
  botui.action.text({ // 显示'text'动作
    action: {
      placeholder: 'Your name'
    }
  });
})
```

这段代码首先会显示一条信息，然后显示一个占位符为`Your name`的输入框。
你可以在这个指南中获取更多相关信息。

## then 的使用

你可能需要在显示一个消息（Message）后再显示另一个消息，或者执行某个动作（Action）后显示信息，因此我们在这里需要回调函数，这里就引入`then`了。你可以在`then`中定义你的回调函数并将其链接到上一条消息或动作（Action）。

举个例子：

```javascript
botui.message.add({ // 显示一条消息
  human: true,
  content: 'Whats your name?'
}).then(function () { // 等待上一条消息显示
  botui.action.text({ // 显示`text`动作
    action: {
      placeholder: 'Your name'
    }
  });
})
```

这里的`then`只能在上一条消息显示后被调用。
使用`then`将消息和动作链接到一起。



```javascript
botui.message.add({ // 显示一条消息
  human: true,
  content: 'Whats your name?'
}).then(function () {  // 等待上一条消息显示
  return botui.action.text({ // 显示`text`动作
    action: {
      placeholder: 'Your name'
    }
  });
}).then(function (res) { // 获取结果
  botui.message.add({
    content: 'Your name is ' + res.value
  });
});
```


> 注意：在第一个`then`中的`return`中，如果你想要保持链接的话，你需要返回一个`Promise`对象. 否则`then`会在前一个消息或动作完成前进行回调。


所有的 `消息` 和 `动作` 方法 都会返回一个 `Promise` 对象，因此我们可以直接使用`.then()` 来将他们链接在一起。