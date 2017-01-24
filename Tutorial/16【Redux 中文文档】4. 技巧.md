### Redux 中文文档
[教程地址：Redux 中文文档](http://cn.redux.js.org/index.html)

---
### 目录
```
1. 介绍
   1.1. 动机
   1.2. 核心概念
   1.3. 三大原则
   1.4. 先前技术
   1.5. 生态系统
   1.6. 示例
2. 基础
   2.1. Action
   2.2. Reducer
   2.3. Store
   2.4. 数据流
   2.5. 搭配 React
   2.6. 示例：Todo List
3. 高级
   3.1. 异步 Action
   3.2. 异步数据流
   3.3. Middleware
   3.4. 搭配 React Router
   3.5. 示例：Reddit API
   3.6. 下一步
4. 技巧
   4.1. 迁移到 Redux
   4.2. 使用对象展开运算符
   4.3. 减少样板代码
   4.4. 服务端渲染
   4.5. 编写测试
   4.6. 计算衍生数据
   4.7. 实现撤销重做
   4.8. 子应用隔离
   4.9. 组织 Reducer
      4.9.1. Reducer 基础概念
      4.9.2. Reducer 基础结构
      4.9.3. Reducer 逻辑拆分
      4.9.4. Reducer 重构示例
      4.9.5. `combineReducers` 用法
      4.9.6. `combineReducers` 进阶
      4.9.7. State 范式化
      4.9.8. Updating Normalized Data
      4.9.9. Reducer 逻辑复用
      4.9.10. Immutable Update Patterns
      4.9.11. 初始化 State
5. 常见问题
   5.1. 综合
   5.2. Reducer
   5.3. 组织 State
   5.4. 创建 Store
   5.5. Action
   5.6. 代码结构
   5.7. 性能
   5.8. React Redux
   5.9. 其它
6. 排错
7. 词汇表
8. API 文档
   8.1. createStore
   8.2. Store
   8.3. combineReducers
   8.4. applyMiddleware
   8.5. bindActionCreators
   8.6. compose
9. react-redux 文档
   9.1. API
   9.2. 排错
10. redux-tutorial
```

---
### 4. 技巧
- 这一章是关于实现应用开发中会遇到的一些典型场景和代码片段。本章内容建立在你已经学会基础章节和高级章节的基础上

#### 4.1 迁移到 Redux
- Redux 不是一个单一的框架，而是一系列的约定和一些让他们协同工作的函数。你的 Redux 项目的主体代码甚至不需要使用 Redux 的 API，大部分时间你其实是在编写函数

#### 4.2 使用对象展开运算符（Object Spread Operator）
- 从不直接修改 state 是 Redux 的核心理念之一, 所以你会发现自己总是在使用`Object.assign()` 创建对象拷贝, 而拷贝中会包含新创建或更新过的属性值
- 尽管这样可行, 但 `Object.assign()` 冗长的写法会迅速降低 reducer 的可读性
- 一个可行的替代方案是使用 ES7 提案的 对象展开运算符。该提案让你可以通过展开运算符 (...) , 以更加简洁的形式将一个对象的可枚举属性拷贝至另一个对象
- 当你在组合复杂对象时, 使用对象展开运算符带来的好处将更加突出
- 目前对象展开运算符提案还处于 ECMAScript Stage 3 草案阶段, 若你想在产品中使用它得依靠转换编译器, 如 Babel

#### 4.3 缩减样板代码
- 将每个 action type 定义为 string 常量
- 人们通常声称常量不是必要的。对于小项目也许正确。 对于大的项目，将 action types 定义为常量有很多好处

#### 4.4 服务端渲染
- 当在服务器使用 Redux 渲染时，一定要在响应中包含应用的 state，这样客户端可以把它作为初始 state

#### 4.5 编写测试
- 因为你写的大部分 Redux 代码都是些函数，而且大部分是纯函数，所以很好测，不需要模拟

#### 4.6 计算衍生数据
- Reselect 库可以创建可记忆的(Memoized)、可组合的 selector 函数。Reselect selectors 可以用来高效地计算 Redux store 里的衍生数据

#### 4.7 实现撤销历史
- 你可以用 Redux 轻而易举地实现撤销历史

#### 4.8 子应用隔离
- 为了使用 React API 来隐藏 Redux 的痕迹，在组件的构造方法里初始化 store 并把它包到一个特殊的组件中

#### 4.9 组织 Reducer
- 一些概念

##### 4.9.1 Reducer 基础概念
- **核心概念**
   *   理解 state 和 state shape
   *   通过拆分 state 来确定各自的更新职责（**reducer 组合**）
   *   高阶 reducers
   *   定义 reducer 的初始化状态

##### 4.9.2 Reducer 和 State 的基本结构
- 首先必须明确的是，整个应用只有一个**单一的 reducer 函数**：这个函数是传给 `createStore` 的第一个参数。
- 一个单一的 reducer 最终需要做以下几件事
   *   reducer 第一次被调用的时候，`state` 的值是 `undefined`。reducer 需要在 action 传入之前提供一个默认的 state 来处理这种情况。
   *   reducer 需要先前的 state 和 dispatch 的 action 来决定需要做什么事。
   *   假设需要更改数据，应该用更新后的数据创建新的对象或数组并返回它们。
   *   如果没有什么更改，应该返回当前存在的 state 本身。

- Redux 鼓励你根据要管理的数据来思考你的应用程序。数据就是你应用的 state，state 的结构和组织方式通常会称为 "shape"
- 在你组织 reducer 的逻辑时，state 的 shape 通常扮演一个重要的角色
- Redux state 中顶层的状态树通常是一个普通的 JavaScript 对象（当然也可以是其他类型的数据，比如：数字、数据或者其他专门的数据结构，但大多数库的顶层值都是一个普通对象）
- 在顶层对象中组织数据最常见的方式是将数据划分为子树，每个顶层的 key 对应着和特定域或者切片相关联的数据

##### 4.9.3 拆分 Reducer 逻辑
- 你可以将 reducer 中的一些逻辑拆分出去，然后在父函数中调用这个新的函数，这些新的函数通常分为三类：
  - 一些小的工具函数，包含一些可重用的逻辑片段
  - 用于处理特定情况下的数据更新的函数，参数除了 `(state, action)` 之外，通常还包括其它参数
  - 处理给定 state 切片的所有更新的函数，参数格式通常为 `(state, action)`

为了清楚起见，这些术语将用于区分不同类型的功能和不同的用例
*   **reducer:** 任何符合 `(state, action) -> newState` 格式的函数（即，可以用做 `Array.reducer` 参数的任何函数）。
*   **root reducer:** 通常作为 `createStore` 第一个参数的函数。他是唯一的一个在所有的 reducer 函数中必须符合 `(state, action) -> newState` 格式的函数。
*   **slice reducer:** 一个负责处理状态树中一块切片数据的函数，通常会作为 `combineReducers` 函数的参数。
*   **case function:** 一个负责处理特殊 action 的更新逻辑的函数。可能就是一个 reducer 函数，也可能需要其他参数才能正常工作。
*   **higher-order reducer:** 一个以 reducer 函数作为参数，且/或返回一个新的 reducer 函数的函数（比如： `combineReducers`, `redux-undo`）

#### 4.9.4 使用函数分解和Reducer组合重构Reducer
>我觉得重构后更加复杂了

#### 4.9.5 使用 `combineReducers`
- 一个常见的问题是 Reducer 在 dispatch action 的时候是否调用了所有的 reducer。当初你可能觉得“不是”，因为真的只有一个根 reducer 函数啊。但是 `combineReducer` 确实有着这样的特殊效果。在生成新的 state 树时，`combinerReducers` 将调用每一个拆分之后的 reducer 和与当前的 Action，如果有需要的话会使得每一个 reducer 有机会响应和更新拆分后的 state。所以，在这个意义上， `combineReducers`会调用所有的 reducer，严格来说是它包装的所有 reducer

- 这里有两种方式来定义 Store state 的初始结构和内容
- 首先，`createStore` 函数可以将 `preloadedState` 作为第二个参数。这主要用于初始化那些在其他地方有持久化存储的 state，例如浏览器的 localStorage
- 另外一种方式是当 state 是 `undefined` 的时候返回 initial state
- `combineReducers` 接收拆分之后的 reducer 函数组成的对象，并且创建出具有相同键对应状态对象的函数。这意味着如果没有给 `createStore` 提供预加载 state，输出 state 对象的 key 将由输入的拆分之后 reducer 组成对象的 key 决定。这些名称之间的相关性并不总是显而易见的，尤其是在使用 ES6 的时候（如默认模块搭配出和对象字面量的简写方向时）

##### 4.9.6  combineReducers 进阶
- 一种解决“共享片段数据更新”的方法是把所需数据当额外参数的形式传递给自定义函数
- 另一种解决“共享片段数据更新” (shared-slice updates) 问题的简单方法是，给 action 添加额外数据。可以通过 thunk 函数或者类似的方法轻松实现

#### 4.9.9 Reducer 逻辑复用
- 正如在 Reducer 逻辑拆分 定义的那样，高阶 reducer 是一个接收 reducer 函数作为参数，并返回新的 reducer 函数的函数

#### 4.9.11 初始化 State
- 主要有两种方法来初始化应用的 state
   - 可以使用 createStore 方法中的第二个可选参数 preloadedState
   - 也可以在 reducer 中为 undefined 的 state 参数指定的默认的初始值。这个可以通过在 reducer 中添加一个明确的检查来完成，也可以使用 ES6 中默认参数的语法 function myReducer(state = someDefaultValue, action)

- 通常情况下，通过 preloadedState 指定的 state 要优先于通过 reducer 指定 state。这样可以使通过 reducer 默认参数指定初始数据显得更加的合理
