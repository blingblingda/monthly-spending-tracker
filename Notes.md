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
4. js 中 should use dynamic data instead of hard data，可以是 http request fetch data 等。这里只能先定义 hard data: expenseDate, expenseTitle, expenseAmount。
