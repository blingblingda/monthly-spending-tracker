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
    **finished Expense Components with static data**
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
   1. 因为这里是用户输入内容并提交的表单，所以整体用表单包裹
   2. 表单中包含两部分，第一部分是 3 个 input 内容区，第二部分是提交按钮。 3) input 区域：第一个 div 放 title 的输入框，第二个 div 放 Amount 的输入框（规定 min&step step 指规定几位小数），第三个 div 放 Date 的输入框（规定 min&max） 4) submit button 区域：div 包裹一个 button type 为 submit
      **create form input section**
5. Listening to and store User Input (get the value the user entered and store that in state.)
   1. 需要监听输入内容，就是每一次改变都要触发 function，因为是自己的改变，所以可以直接拿 event 的属性即可拿到输入内容。onChange+event 组合，即可拿到用户输入框输入数据。
   2. 使用 useState 存储拿到的数据。(用两种写法，逐条写或者合并到一个 useState 里写)
6. Handling form submission
   1. 不要直接在 button 上加 onClick 事件。这种放在 form 里面的、type 为 submit 的 button，提交事件函数应该放在 form 里 onSubmit
   2. 使用 event 里自带的 preventDefault 方法: we can stay on the current loaded page without sending any request anywhere, and can continue handling this with JS.
   3. const 一个对象 expenseData,存放三个最新状态（注意时间需要转换为 default 格式）
   4. 提交后自动清空 input：two-way binding: for inputs we don't just listen to changes, but can also pass a new value back into the input. so we can reset or change the input programmatically.
   5) 给 input 增加 value 属性，等于目前 state
   6) 在 submitHandler function 中，当收集了所有 state 之后，再使用 setState 把所有 state 归为‘’，这样 value 一等就等于‘’了。
      **gather expenseData and clear inputs**
7. Pass the data (collecting and generating in expense form) to the app component. 子传父
   1. 父组件里的子组件标签设置需要传递的事件 onSaveExpenseData，每次子组件中调用该事件，则触发对应函数 saveExpenseDataHandler
   2. 定义该处理函数, 该函数被触发后会收到一个子组件传过来的一个参数 enteredExpenseData, 真正存起来的 data 应该是除了子组件拿过来的 3 个内容之外还要增加一个 id，因此在函数体中 const 一个新对象 expenseData，里面存储收过来的 enteredExpenseData 的所有内容，以及新增一个 id。这样 expenseData 就是我们最终需要的 data 了。
   3. 因为父组件把该处理函数以 onSaveExpenseData 的方式传递给了子组件，因此在子组件中首先用 props 接收函数，然后在最后提交的 submitHandler 中调用，把收集整理好的 expenseData 放进去就可以传递给父组件了。
8. 把最终版的 expenseData 传递给 App 的数据组中。
   1. 定义一个处理函数用于接收子组件的数据并增加到父组件 App 数据库中。
   2. 把该处理函数通过名字 onAddExpense 传给 NewExpense 组件。
   3. 到子组件 NewExpense 中接收并 call 这个函数，把要传递的信息作为参数传过去。passing data to that function, we are lifting that data that state up, we are not keeping it in NewExpense component, instead, we are lifting it up to the App component. Lifting State Up: moving data from a child component to some parent component to either use it there or to then pass it down to some other child component.

## 新增 ExpenseFilter

1. 给 select tag 增加监听事件拿到用户所选年份
2. 把 filter 组件插入 expense 组件中
3. 在 expense 组件中设定一个接收函数，并把这个函数传给 filter 组件。
4. filter 接收这个函数，把用户选择的年份作为参数传过去
5. expense 接到这个参数，并把它更新在相应的 state 中。注意，filter 组件只负责拿到并传送用户选择的年份，并不负责储存年份。年份应该被储存在父组件 expense 中。
6. 如何把 expense 中 useState 的 default year 显示在 filter 里面
   1. 把当前的 filteredYear 传给 Filter 组件
   2. 在 filter 组件中显示 select 时，给定一个 value 属性为接收到的 filteredYear
7. filter 其实并没有函数逻辑在里面，他只是输出展示页面，真正的 function 和逻辑提取数据储存都在父组件 expense 中，filter 只是接受了父组件定义好的函数，把自己的参数传进去而已。
8. dumb&smart component， stateless&state component:只是名字状态不同，一个没有包含管理 state，一个有管理 state 而已。
   **Lifting State up among ExpForm NewExp and App**
9. quiz：
   1. How can you communicate from one of your components to a parent (i.e. higher level) component?
      you can accept a function via props and call it from inside the lower-level(child) component to then trigger some action in the parent component (which passed the function)
   2. Why do you need this extra "state" concept instead of regular JS variables which you change and use?
      Because standard JS variables don't cause React components to be re-evaluated
   3. What's wrong about this code snippet?

```
const [counter, setCounter] = useState(1);
...
setCounter(counter + 1);
```

      If you update state that depends on the previous state, you should use the "function form" of the state updating function instead.

## render Expense list

1. 动态显示已有的 expenses 列表。render Expenses dynamically
   1. 目前在 Expenses 组件中展示 ExpenseItem 的方法是逐一列出然后分别传参，需要改为根据 App 组件传过来的数据 array 动态生成
   2. 拿到 App 传过来的数据组，在该数组的基础上使用 map 把每一个对象逐一转换成所需要的 JSX 展示格式(注意用 map 的话需要在转换后的内容里增加 key)
2. 动态插入新增 expense 到原有 expenses 列表
   1. 把之前 dummyExpense 拿出去，在组件中建立 state，default 是 dummyExpense
   2. 之前已经写过把子组件中新增的那个 expense 传到 app 里，但是把这条 expense 增加到 state 里面呢？if you update your state depending on the previous state, you should use this special function form for this state updating function. 不能直接用[xx, ...xxx]的形式，应该是 prevExpenses => {return[xx, ...prevExpenses]}
   3. add key to help React identify the individual items.
3. 按照所选年份筛选 expense list
   1. 一开始的思路反了，本来是想在已经 map 好的 list 中用 filter 筛出符合 year 条件的 expense，但问题是如果已经 map 好了说明 data 的格式已经成功转换为 JSX 显示 component，其实就不是 array 的 data 也就没办法 filter 了。因此应该先用 filter 从 App 传过来的原始 items array 中把符合条件的筛出来组成新的 array，之后再用 map 把这部分 array transfer 成 component 格式。
   2. const 一个 filteredExpense 的 array，用 filter 筛出符合条件的
   3. 对这个新 array 进行 map
      **render and filter expense list dynamically**

## outputing conditional content

1. 诉求：filter 的年份有东西时展示相应年份的 ExpenseItem，没有东西的时候展示一句话。
2. 写法一：在最外层加一个三元表达式，如果 filterExpenses 的 length 为 0 就显示一个 p tag，否则就正常 map component.

```
        {filteredExpense.length === 0 ? (
          <p>No expenses found</p>
        ) : (
          filteredExpense.map((expense) => (
            <ExpenseItem
              key={expense.id}
              title={expense.title}
              amount={expense.amount}
              date={expense.date}
            />
          ))
        )}
```

3. 写法二 abusing here: 使用&&连接。react 中如果前面 true，则显示&&后面的内容。这样可以避免三元表达式过长的问题，变成两个 condition.

```
        {filteredExpense.length === 0 && <p>No expenses found</p>}
        {filteredExpense.length > 0 &&
          filteredExpense.map((expense) => (
            <ExpenseItem
              key={expense.id}
              title={expense.title}
              amount={expense.amount}
              date={expense.date}
            />
          ))}
```

4. 写法三：不要把逻辑直接卸载 return 里面，提炼到外面。一开始 const 一个变量 expensesContent，在外面用逻辑定义好这个变量的内容，return 里面直接展示该变量即可。

```
return上面：
let expenseContent = <p>No expenses found.</p>;
  if (filteredExpense.length > 0) {
    expenseContent = filteredExpense.map((expense) => (
      <ExpenseItem
        key={expense.id}
        title={expense.title}
        amount={expense.amount}
        date={expense.date}
      />
    ));

return里面
        {expenseContent}
```

5. 为了让 Expenses 更清晰，可以把 list 这一块单独拿出来。之前是 Expenses ->ExpenseItem，现在改为 Expenses -> ExpensesList -> ExpenseItem
   1. Expenses 中把 filter 出来待 map 的 data 传递给 ExpensesList 组件
   2. 在新的 ExpensesList 组件中稍微修改一下逻辑。在 return 的上面单独给一个 if 判断，如果没有数据，那么 return 一个 h2 标签（单独写样式）。这样正常的 return 正好就变成了 if 里面否则的 return，那么外面不要包 div，包一个 ul 给个样式，里面是 map 出的组件内容。
   3. 由于在 list 里面用的是 ul 包裹每一个 expenseItem，所以在 item 组件中最外层应该由 li 包裹一下。
6. default 是有两个 button：cancel+add expense，提交表单之后变成中间一个 Add New Expense 的按钮。
