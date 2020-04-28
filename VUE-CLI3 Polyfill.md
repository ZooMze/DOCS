<!--
 * @Author: your name
 * @Date: 2020-04-28 14:10:06
 * @LastEditTime: 2020-04-28 14:29:20
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \vue-codechos-templatec:\project\DOCS\VUE-CLI3 Polyfill.md
 -->
# Vue-Cli3 set polyfill
## browserslist
脚手架已在`package.json`配置了`browserlist`字段, 该字段制定了在哪些范围下应用ployfill
这个值会被 [@babel/preset-env](https://babeljs.io/docs/en/next/babel-preset-env.html) 和 [Autoprefixer](https://github.com/postcss/autoprefixer)  用来确定需要转译的 JavaScript 特性和需要添加的 CSS 浏览器前缀

## polyfill
一个默认的 Vue CLI 项目会使用 [@vue/babel-preset-app](https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/babel-preset-app)，它通过 `@babel/preset-env` 和 `browserslist` 配置来决定项目需要的 polyfill

默认情况下，它会把 `useBuiltIns: 'usage'` 传递给 `@babel/preset-env`，这样它会根据源代码中出现的语言特性自动检测需要的 polyfill。这确保了最终包里 polyfill 数量的最小化, 实现了按需添加polyfill。**然而，这也意味着如果其中一个依赖需要特殊的 polyfill，默认情况下 Babel 无法将其检测出来**

`useBuiltIns` 的可选值: 
`usage`: 自动检测源码中使用的代码特性自动检测添加polyfill
`entry`: 根据`browserslist`, 进行添加polyfill
`false`: 忽略`browserslist`, 如果手动引入了polyfill, 则应用全部

