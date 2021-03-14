---
title: 安装
---

## 安装


### 使用CDN

一个BotUI页面需要以下文件。你可以直接在你的页面中使用以下链接

```
// 引入基本布局
https://unpkg.com/botui/build/botui.min.css

// 默认主题 - 你可以创建自己的主题
https://unpkg.com/botui/build/botui-theme-default.css

// Vue - BotUI 需要页面中有 Vue.js
https://cdn.jsdelivr.net/vue/latest/vue.min.js

// BotUI - 主文件
https://unpkg.com/botui/build/botui.min.js

```


### NPM 安装

```bash
npm install botui --save
```

根据所需，将`build`文件夹下的文件引入。

你可能需要以下文件：

```
node_modules/botui/build/botui.min.css
node_modules/botui/build/botui-theme-default.css
node_modules/botui/build/botui.js
```

### 使用 Webpack

在 webpack 或 rollup 中,你也需要同时 `import` Vue.

```javascript
import Vue from 'vue'
import BotUI from 'botui'

const botui = BotUI('my-botui-app', {
  vue: Vue // 传递依赖
})
```

> 确定使用 Vue 的 min（压缩） 版本。 完整版的不知道为啥有错误。 

你可以在webpack的`config`中添加一个`alias`：
```javascript
module.exports = {
  ...
  resolve: {
    alias: {
      'vue': 'vue/dist/vue.min.js',
    }
  },
  ...
}
```


如果你不能添加 `alias` （比如你使用[`create-react-app`](https://github.com/facebook/create-react-app)）, 请编辑 Vue 的 `package.json` 文件中的 `module` 值指向`vue.min.js` 而非 `vue.runtime.esm.js`：

```
"module": "dist/vue.min.js",
```

你也可以通过 CLI 操作:
```
sed -i '' 's_vue.runtime.esm.js_vue.min.js_g' ~/__PATH_TO_YOUR_APP__/node_modules/vue/package.json
```

请注意，每次将Vue作为npm包添加或升级到你的项目时，都需要执行此手动步骤。
### 本地下载

你可以从 [Github repo](https://github.com/moinism/botui/) 下载最新的文件 然后引入你的项目。
所有的依赖项都在 `build` 文件夹。但是你仍需要通过CDN或本地文件引入 [Vue](https://cdn.jsdelivr.net/vue/latest/vue.min.js)。

包含所有依赖文件的基本页面大概是这样的：
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>BotUI</title>
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
    <link rel="stylesheet" href="./botui/build/botui.min.css" />
    <link rel="stylesheet" href="./botui/build/botui-theme-default.css" />
  </head>
  <body>

    .....

    <script src="https://cdn.jsdelivr.net/vue/latest/vue.min.js"></script>
    <script src="./botui/build/botui.min.js"></script>
  </body>
</html>
```

### bot-ui 标签

`<bot-ui>` 标签是我们一切开始的地方：

在页面中引入所有依赖文件后，现在你可以通过添加 `<bot-ui>` 标签在你需要的地方显示Bot，例如：

```html
<div id="my-botui-app">
  <bot-ui></bot-ui>
</div>
```

然后BotUI会把需要的节点填入 `#my-botui-app` 所在元素。 你就能在此处看见你的Bot了。
### 初始化 BotUI

添加`<bot-ui>`后，再进行最后一步就可以完成安装了。

```javascript
var botui = new BotUI('my-botui-app');
```

安装正确的情况下，`BotUI` 应为页面中的全局变量以传递拥有`<bot-ui>`标签的元素的id。

就这样了，现在你可以开始添加消息和显示动作了。