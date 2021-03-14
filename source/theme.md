---
title: 主题
---

# BotUI 主题

创建BotUI的自定义主题很简单。

## 创建你自己的主题

1. Clone the [git repo](https://github.com/moinism/botui).
2. `cd` clone 的 文件夹。
3. 执行 `npm install`
4. 执行 `gulp watch`
5. 进入 `src/styles/themes` 文件夹
6. 复制 `default.scss` 然后重命名，例如 `custom.scss`
7. 现在你可以更改 `custom.scss` 的样式内容然后保存文件
8. 进入 `build` 文件夹，你会看见 `botui-theme-custom.css` 文件
9. 复制它到你的项目文件夹，代替 `botui-theme-default.css`

10. 完工。


## 结构



#### HTML

这是初始化BotUI后html的样子：

```html
<div class="botui botui-container">
  <div class="botui-messages-container">
    <div class="botui-message"> <!-- 这个元素还可以通过 'cssClass' to 'message' 应其他类 -->
      <div :class="[{human: msg.human, 'botui-message-content': true}, msg.type]"> <!--  -->
        <span></span> <!-- 如果type是text，文本会出现在这 -->
        <iframe></iframe> <!-- 如果type为embed -->
      </div>
    </div>
  </div>
  <div class="botui-actions-container">
    <div>
        <form class="botui-actions-text" :class="action.cssClass">  <!--  -->
        <input class="botui-actions-text-input" :class="action.text.cssClass" required/> <!--  -->
        <button class="botui-actions-text-submit">Go</button> <!--只会在移动设备显示 -->
        </form>
        <div class="botui-actions-buttons" :class="action.cssClass"> <!--  -->
          <button :class="button.cssClass" class="botui-actions-buttons-button"> <!--  -->
          <i class="botui-icon botui-action-button-icon fa" :class="'fa-' + button.icon"></i> <!--  -->
          <!-- button text -->
        </button>
      </div>
    </div>
  </div>
</div>
```

#### SCSS

你可以按照此结构在自己的主题中自定义BotUI。

```css

.botui-container {

}

.botui-messages-container {
}

.botui-actions-container {
}

.botui-message {

}

.botui-message-content {

  &.human {

  }

  &.text {
  }

  &.embed {

  }
}

.botui-message-content-link {
}

.botui-actions-text-input {

}

.botui-actions-text-submit {

}

.botui-actions-buttons-button {

}

```
