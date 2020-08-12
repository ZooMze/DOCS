# React

## JSX1111111111111

`const element = <h1>Hello, world!</h1>;`

既不是字符串也不是 HTML, 是一个 JavaScript 的语法扩展, JSX 可以很好地描述 UI 应该呈现出它应有交互的本质形式。 

```
const name = 'Josh Perez';
const element = <h1>Hello, { name } </h1>;

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

大括号内放置任何有效的 JavaScript 表达式。

**SX 也是一个表达式**

可以在 if 语句和 for 循环的代码块中使用 JSX，将 JSX 赋值给变量，把 JSX 当作参数传入，以及从函数中返回 JSX
```
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

**Babel 会把 JSX 转译成一个名为 `React.createElement()` 函数调用。**
```
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
// 上下等效
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

## 元素的渲染

根节点内的所有内容都将由 React DOM 管理, 同Vue实例: 架构产生单页应用 , 引用则可以产生多个实例

### 更新元素

React 元素是**不可变对象**。一旦被创建，你就无法更改它的子元素或者属性。一个元素就像电影的单帧：它代表了某个特定时刻的 UI。
更新 UI 唯一的方式是创建一个全新的元素，并将其传入 `ReactDOM.render()`。
```
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById('root'));
}

setInterval(tick, 1000);
```
上例为一个简单计时器, 但 **React 只更新它需要更新的部分**, 在state部分会对此进行优化

## 组件 & Props

概念上类似于 JavaScript 函数。它接受任意的入参（即 “props”），并返回用于描述页面展示内容的 React 元素

```
// 通常的定义方式
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
// 上下等效
// 使用ES6的class
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```
React 元素也可以直接引用 组件 `const element = <Welcome name="Sara" />;`
多个组件可以任意嵌套, 

**注意： 组件名称必须以大写字母开头。**

**Props 只读**

不修改入参的函数称为 **纯函数**, 所有React组件都不应该修改入参, state可以辅助完成被纯函数限制的内容

## state

### 将函数组件转换成 class 组件