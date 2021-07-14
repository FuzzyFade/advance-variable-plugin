[English](./README.md) | 简体中文

## Define Runtime Variable Plugin

> 在 loader 之后注入代码的插件（仅支持 webpack5）

### 使用方法

webpack 配置文件  (eg: webpack.config.js)
```js
import DefineVariablePlugin from 'define-runtime-variable-plugin'

module.exports = {
  ...
  plugins: [
    ...
    new DefineVariablePlugin({
      getCode: () => `const time = ${new Date()}`
    }),
  ]
}
```

工程代码
```tsx
import React from 'react'

// 此 time 的时间大于 loader 结束的时间
const App = () => {
  return <div>{time}</div>
}
```

### 特性

Webpack 自带的 [DefinePlugin](https://www.webpackjs.com/plugins/define-plugin/) 不能够做到在 loader 之后获取代码并注入到 loader 产物的能力。

而本插件能够做到将 loader 阶段处理和计算的一些产物的数据通过某种形式在 loader 之后注入到产物代码当中，使得在代码运行时能够拿到数据。

### 参数

|  参数名   |  默认值  |  是否必选  | 备注  |
| ---- | ---- | ---- | ---- |
| getCode  | - | ✅ | 会在相应阶段触发回调注入该函数返回值于代码中 |
| filter  | `(name) => name.includes('.js')` | - | 判断产物的哪些文件需要注入该段代码 |