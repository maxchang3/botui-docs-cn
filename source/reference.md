---
title: API 参考
---

# API 参考

- [API 参考](#api-参考)
  - [构造函数](#构造函数)
      - [参数](#参数)
  - [botui 实例](#botui-实例)
    - [botui.message](#botuimessage)
    - [botui.action](#botuiaction)
    - [message object](#message-object)
    - [action object](#action-object)
    - [text object](#text-object)
    - [button object](#button-object)
    - [result object](#result-object)
  - [promise](#promise)

## 构造函数

`BotUI`的构造函数会返回一个[`BotUI` 实例](#botui-instance).
#### 参数
  - `id` - _必须_ - 拥有 `<bot-ui>` 标签的元素的id.
  - `options` - _可选_ -  选项的一个 `对象`

  ```javascript
  // 默认值的选项
  {
    debug: false, // 如果想使用底层Vue的debug，请设置为true
    fontawesome: true, // 项目中如果已经引入 FontAwesome 请设置为false，否则会重复引用。
  }
  ```

## botui 实例

该实例拥有两个属性：

  - [`message`](#botui.message)  （消息）
  - [`action`](#botui.action)    （动作）


### botui.message

该方法用于UI中消息的增、删、改。
它拥有7个方法：

- #### `botui.message.add`
  在UI中添加消息。

  接受 [`message`](#message-object) 类型的 `对象`。

  返回带有添加消息`index` 的 [`Promise`](#promise) 。
- #### `botui.message.bot`
  在UI中添加消息。 是 `message.add`的简写。

  接受 [`message`](#message-object) 类型的 `对象`。

  返回带有添加消息`index` 的 [`Promise`](#promise) 。

- #### `botui.message.human`
  在UI中添加消息，设置 `human` 为 `true`.

  接受 [`message`](#message-object) 类型的 `对象`。

  返回带有添加消息`index` 的 [`Promise`](#promise) 。


- #### `botui.message.get`

  接受 [`message`](#message-object) 的 `index`

  返回带有 [`message`](#message-object) 实例的 [`Promise`](#promise)。

- #### `botui.message.update`
  在UI中更新消息。

  接受两个参数：
  1. `index`
  2. [`message`](#message-object)

  > 只能更新消息的 `content` 和 `loading` 属性。无法更改类型。

  返回带有更新 `内容` 的 [`message`](#message-object) 的 [`Promise`](#promise)。

- #### `botui.message.remove`
  在UI中删除消息。

  接受需要删除 [`message`](#message-object) 的 `index`。

  > 谨慎使用。 它会修改所有消息的内建`index`。 可能会导致`message.update`出现奇怪的现象。

  返回 [`Promise`](#promise).

- #### `botui.message.removeAll`
  删除UI中的所有消息。

  返回 [`Promise`](#promise).

### botui.action

该方法可以用于在UI中显示、隐藏、设置需要执行的动作。

它有4个方法

  - #### `botui.action.show`
    显示动作。

    接受 [`action`](#action-object) 类型的 `实例`。

    返回 [`Promise`](#promise)

  - #### `botui.action.hide`
    隐藏动作，不需要任何参数。

    返回 [`Promise`](#promise)

  - #### `botui.action.text`
    显示动作，并且设置动作的 `type` 为 `text`（文本）。是`show`的简写。

    接受[`action`](#action-object)类型的`实例`。

    返回带有[`result`](#result-object) 的 [`Promise`](#promise) 。

  - #### `botui.action.select`
    显示动作，并且设置动作的 `type`为`select`（选择框）。 是`show`的简写。

    接受[`action`](#action-object)类型的`实例`。

    返回带有[`result`](#result-object) 的 [`Promise`](#promise) 。

  - #### `botui.action.button`

    显示动作，并且设置动作的`type`为`button`（按钮）。是`show`的简写。

    接受[`action`](#action-object)类型的`实例`。

    返回带有[`result`](#result-object) 的 [`Promise`](#promise) 。

### message object

可以传递给……

```javascript
// 使用默认值

{
  loading: false, // 如果想显示三个动点的加载动画请设置为true。仅在 >= 0.3.1版本。

  delay: 0, // 延迟显示消息，单位为毫秒。

  type: 'text', // 可以为 'text' 或 'embed'

  content: '', // 若上述类型为 'embed' 应为URL, 否则应为文本。

  human: false, // 右对齐。

  cssClass: '', //  一个或一组class类名。
}
```

### action object

可以传递给 `botui.action.show`, `botui.action.text` 以及 `botui.action.button`。

```javascript
// 使用默认值
{
  type: 'text', // 'text' （文本）或 'button'（按钮）

  action: [], // 若类型为按钮（button），则应该为按钮实例的列表，否则则是文本（text）列表。

  cssClass: '', // 一个或一组class类名。

  autoHide: true, // 提交后是否自动隐藏。

  addMessage: true // 动作添加的消息是否添加到用户一侧（右侧）。
}
```

### text object

作为 `action` 实例中 `action` 的必须项。 

```javascript
{
  size: 30, // 要显示的输入框的大小。依赖于输入元素的HTML size属性。

  sub_type: '', // 可以是任何html input元素的有效类型，例如： number, tel, time, date, email 等。

  value: '', // 预填充内容，仅适用于文本（type）类型。

  placeholder: 'Write here ..', // 设置输入元素的占位符。
}
```

### button object

作为 `action` 实例中 `action` 数组的必须项。

```javascript
{
  icon: '', // 按钮所显示的图标。
  text: '', // 按钮所显示的文职。
  value: '', // this is how you will identify the button when result is returned. 返回结果时用来区分按钮。

  cssClass: '' // 一个或一组class类名。

}
```


### result object

作为参数传递给`action`方法返回的`Promise`。
 

```javascript
{
  type: '', // 从中返回的操作的“Text”或“Button”类型。

  value: '', // 若类型为text，则应为文本，若为按钮，则应与按钮实例的`value`值一致。

  text: '' // 仅当消息类型为“按钮”时才存在。与按钮对象中的“文本”相同。
}
```

## promise

这是一个始终返回 _resolve_ 的 JavaScript <a href="https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Promise" target="blank">`Promise`</a>.

这意味着你不需要 `catch`, 只需要用 `then` 接受回调内容。
