## Set up

1. download Node.js
2. run "npx create-react-app my-app" -> npm start
3. src: index.js, index.css, App.js

```
import React from "react";
import ReactDOM from "react-dom/client";

import "./index.css";
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<App />);
```

```
function App() {
  return (
    <div className="App">
      <h2>Let's get started!</h2>
    </div>
  );
}

export default App;
```

## Expense Components

1. src 下建一个 components folder, index.js 和 App.js 还放在外面
2. 新建 ExpenseItem.js 并导入 App，每个 component 里的 return 里面需要用一个大 div 包裹全部
3. 新建 ExpenseItem.css 与 js 相对应，并引入相应 js
4. js 中 should use dynamic data instead of hard data，可以是 http request fetch data 等。这里只能先定义 const variable: expenseDate, expenseTitle, expenseAmount。**ExpenseItem with const variable**

   1. new Date 出来的数据是 object，需要使用 toISOString()方法转换成 string 才能显示。
   2. Components can't just use data stored in other component, need to pass data via "Props"
   3. 如果把举例数据写在 ExpItem 组件中，则 App 组件中复制多组 ExpItem 内容均相同，因此应该把数据写在 App 组件中（父组件），然后使用 props 分别传给 ExpItem 来展示。(第一步拿到/设置数据 array，第二步通过子组件标签传递需要的属性)

5. 第三步到子组件中用 props 来收取属性，是一个 object，然后在 return 里面相应位置插入相应 props 属性. **use props to pass data from App to ExpItem and display**
6. 调整 ExpItem 中日期显示格式

   1. 把目前一长串数字拆成 3 个 div 分别显示月日年
   2. 月日使用 toLocaleString function 显示，年直接用 getFullYear function 显示
   3. 在上面 const 好，return 的 div 里只放 variable

7. 新建一个子组件 ExpenseDate，把日期相关 div 拆出来单独存放

   1. props 需要在 ExpItem 处中转一下,直接把 date 整体传过去即可
   2. 新建相应 css,并引入 js,在 js 中给相应 tag 加 className 以展示 css **make Date as a single component and added css**

8. 新建 Expenses 组件，把 App 里面 4 个 Expenses 统一拿出来单独放在 Expenses 里，App 穿的时候改个名字别用 expenses=expenses，用 items
9. The concept of "Composition" (children props, wrap component)
   1. this approach of building a user interface from smaller building blocks is called composition.
   2. we have HTML structure duplication (Expenses 和 ExpenseItem 外层均有单独的 div 包裹) and style duplication (其中 border-radius 和 box-shadow 的给是内容是重复的)。now we want to create a component which actually just serves as a shell around any kind of other content.
      1. 把重复的两个 div 整理成一个放到新组件 Card 中，因为是插在 Expenses 和 ExpItem 里面包裹用的所以也需要接收 props，然后在返回的 div 里面放{props.children}，这样在使用的时候就可以把内容传递过去了。
      2. 新建一个对应的 Card.css，把重复的 css 放进来。原来两个 css 中的重复内容就可以删掉了。但注意在两个 component 中使用 card 时，className 需要同时使用 card 公用+自己独立的，不然 card 公用的 css 不生效。所以需要在 Card.js 里面 const 一个合并的 classes，然后引入 div，这样别的组件直接用就可以了。
   3. we are able to extract some code duplication from inside CSS code and HTML code and JSX code into this separate wrapper component, which allow you to save a lot of code duplication and keep your other components clean.
10. 把 component 按照 UI 和功能分文件夹，另外引入 react 还是必要的。可以把所有 function 换成 arrow function。
11. quiz:
    1. which kind of code do you write when using React.js?
       Declarative JavaScript Code. With React.js, you define the "goal" (i.e. what should be shown on the screen) and let React figure out how to get there.
       You would write imperative JS code when writing a regular JS app (without React) (React vs vanilla JavaScript).
    2. What is JSX?
       It's a special, non-standard syntax which is enabled in React projects. React projects like the ones we create via "create-react-app" support JSX syntax. It gets compiled to standard JS code behind the scenes
    3. Why is React all about "Components"?
       Every UI in the end up is made up of multiple building blocks (=components), hence it makes sense to think about user interfaces as "combinations of components"
    4. What is a "React Component"?
       It's a JS function which typically returns HTML(JSX) code that should be displayed.
    5. What does "component tree" means?
       It means that you have a root node which then has more components nested beneath it.
    6. How can you output dynamic data in React components (i.e. in the returned JSX code)?
       You can use single curly braces with any JS expression between them.

## 新增 Form input

1. 每个 Item 后面增加一个 button，点击 button 改变 title 内容
   1. 增加 button，添加点击事件
   2. 用 useState 拿到 title，并拆解为
   3. 在事件处理函数中，使用 setTitle 改变 title 状态。
   4. 更新 return 显示内容
2. 新建 NewExpense 文件夹存放与用户新增 expense 的表单数据文件
3. 新建 NewExpense 组件，引进相应 css，目前仅 return 一个 ExpenseForm 组件。因该组件与 Expense 大组件平行，在 App 中插入即可显示。
4. 新建 ExpenseForm 组件
   1）因为这里是用户输入内容并提交的表单，所以整体用表单包裹
   2）
