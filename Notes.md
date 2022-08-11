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

## ExpenseItem Components

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
   2. 新建相应 css,并引入 js,在 js 中给相应 tag 加 className 以展示 css
