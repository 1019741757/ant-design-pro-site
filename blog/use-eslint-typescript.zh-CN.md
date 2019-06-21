---
order: 1
title: 一起来用 eslint 吧
type: Blog
time: 2019-06-21
---

在 TypeScript 中我们一直使用 tslint 来对我们的代码质量进行保障。但是 tslint 是 eslint 的子集。tslint 大概提供了 151 条基础规则，eslint 却有  249 条，更不用说 eslint 发达的生态了，提供了更多的规范代码。tslint 团队也发现了这个问题，并且决定[转移](https://eslint.org/blog/2019/01/future-typescript-eslint)到 eslint 中。

## 起因

在 Pro v4 的筹备中，我们增加了一个功能，将 typescript  转化为 javascript 的 功能，转化完成之后我们跑了一遍 eslint 和 prettier 来让代码更像是人写的。结果转化完成之后的 js 代码无法通过 eslint 的检查:

比如这里：

![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/93819/1561039456413-1a389431-a7ff-4b00-b872-8f34249bab35.png#align=left&display=inline&height=159&name=image.png&originHeight=318&originWidth=2848&size=96918&status=done&width=1424)

还有这里：

![image.png](https://intranetproxy.alipay.com/skylark/lark/0/2019/png/93819/1561039496763-22b0d0d8-172b-4b74-b50d-908a47024d22.png#align=left&display=inline&height=474&name=image.png&originHeight=948&originWidth=2238&size=175958&status=done&width=1119)

## 结果

如果我们使用的是 eslint，这些问题应该会直接暴露。于是开始进行了调研和使用。首先在 Pro 中尝试了一把。效果很不错，具体可以看这个 [PR](https://github.com/ant-design/ant-design-pro/pull/4336)。一鼓作气我在[pro-blocks](https://github.com/ant-design/pro-blocks/pull/28) 中也加入了这个 lint。

我们将这些规则发布成了一个包   🌟🌟**umi-fabric** 🌟🌟, 这个库提供了 eslint ，stylelint 和 prettier 的一些预设，非常适合所有人使用。所有打开的规则都是对提升代码质量有意义的。

## 使用

**umi-fabric **的使用非常简单。

```bash
npm install eslint @umijs/fabric -save-dev
```

并且在根目录 `.eslintrc.js`  中做如下配置。

```tsx
const fabric = require('@umijs/fabric');

module.exports = fabric.eslint;
```

在 vscode 中 eslint 的插件并不会默认的去 lint .ts 文件，我们需要在 `settings.json`  中设置

```jsx
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "typescript",
    "typescriptreact"
  ],
```

接下来就可以愉快的使用了。使用 `eslint fix`  一下老的 ts 代码有奇效哦。
