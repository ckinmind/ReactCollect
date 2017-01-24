### # Redux 常见问题
[教程地址：Redux 常见问题](http://cn.redux.js.org/index.html)

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
### 5.1 Redux 常见问题：综合
- **何时使用 Redux**
  - 在打算使用 Redux 的时候进行权衡是非常重要的。它从设计之初就不是为了编写最短、最快的代码，他是为了解决 “当有确定的状态发生改变时，数据从哪里来” 这种可预测行为的问题的
  - 如果你只是刚开始学习 React，你应该首先专注于 React，然后再看看 Redux 是否适合于你的应用
  - 最后需要说明的是：Redux 仅仅是个工具。它是一个伟大的工具，经常有一个很棒的理由去使用它，但也有很多的理由不去使用它。时刻注意对你的工具做出明确的决策，并且权衡每个决策带来的利弊

### 5.2 Redux 常见问题：Reducer
- 许多用户想在 reducer 之间共享数据，但是 `combineReducers` 不允许此种行为。有许多可用的办法
   *   如果一个 reducer 想获取其它 state 层的数据，往往意味着 state 树需要重构，需要让单独的 reducer 处理更多的数据。
   *   你可能需要自定义方法去处理这些 action，用自定义的顶层 reducer 方法替换 `combineReducers`。你可以使用类似于reduce-reducers 的工具运行 `combineReducers` 去处理尽可能多的 action，同时还要为存在 state 交叉部分的若干 action 执行更专用的 reducer。
   *   类似于 `redux-thunk` 的异步 action 创建函数 能通过 `getState()` 方法获取所有的 state。 action 创建函数能从 state 中检索到额外的数据并传入 action，所以 reducer 有足够的信息去更新所维护的 state 层

### 5.3 Redux 常见问题：组织 State
- **必须将所有 state 都维护在 Redux 中吗？ 可以用 React 的 `setState()` 方法吗**
  - 没有 “标准”。有些用户选择将所有数据都在 Redux 中维护，那么在任何时刻，应用都是完全有序及可控的。也有人将类似于“下拉菜单是否打开”的非关键或者 UI 状态，在组件内部维护。适合自己的才是最好的
  - 使用局部组件状态是更好的。作为一名开发者，应该决定使用何种 state 来组装你的应用，每个 state 的生存范围是什么。在两者之间做好平衡，然后就去做吧
  - 有许多开源组件实现了各式各样在 Redux store 存储独立组件状态的替代方法

### 5.4 Redux 常见问题：创建 Store
>略

#### 5.5 Redux 常见问题：Action
>略

#### 5.6 Redux 常见问题：代码结构
- 因为 Redux 只是数据存储的库，它没有关于工程应该被如何组织的直接主张。然后，有一些被大多数 Redux 开发者所推荐的模式：
  *   Rails-style：“actions”、“constants”、“reducers”、“containers” 以及 “components” 分属不同的文件夹
  *   Domain-style：为每个功能或者域创建单独的文件夹，可能会为某些文件类型创建子文件夹
  *   “Ducks”：类似于 Domain-style，但是明确地将 action、 reducer 绑定在一起，通常将它们定义在同一文件内

#### 5.7 Redux 常见问题：性能
>略

#### 5.8 Redux 常见问题：React Redux
>略

#### 5.9 Redux 常见问题：其它
- 如何在 Redux 中实现鉴权
