English | [简体中文](./README_zh-CN.md)

## Advance Define Plugin

> A Plugin that injects code after loader (required webpack5)

### Usage

webpack.config.js
```js
import AdvanceDefinedPlugin from '@icecee/advance-define-plugin'

module.exports = {
  ...
  plugins: [
    ...
    new AdvanceDefinedPlugin({
      getCode: () => `const time = ${new Date()}`
    }),
  ]
}
```

project component code
```tsx
import React from 'react'

// This `time` is greater than the end time of loader
const App = () => {
  return <div>{time}</div>
}
```

### Feature

[DefinePlugin](https://www.webpackjs.com/plugins/define-plugin/) can't get the code after the loader and inject it into the loader product.

**AdvanceDefinedPlugin** can inject the data of some products processed and calculated in the loader stage into the build code after the loader, so that the data can be obtained (or function call) when the code runs.

### Options

|  option   |  default  |  required  | comment  |
| ---- | ---- | ---- | ---- |
| getCode  | - | ✅ | The callback will be triggered at the corresponding stage to inject the return value of this function into the code |
| filter  | `(name) => name.includes('.js')` | - | Determine which files (build files) of the product need to be injected with this code |