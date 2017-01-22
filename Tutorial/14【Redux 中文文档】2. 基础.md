### Redux 中文文档
[教程地址：Redux 中文文档](http://cn.redux.js.org/index.html)
[英文原版](http://redux.js.org/)

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
### 2. 基础
- 不要被各种关于 reducers, middleware, store 的演讲所蒙蔽 —— Redux 实际是非常简单的。如果你有 Flux 开发经验，用起来会非常习惯。没用过 Flux 也不怕，很容易

#### 2.1 Action
- **Action** 是把数据从应用（译者注：这里之所以不叫 view 是因为这些数据有可能是服务器响应，用户输入或其它非 view 的数据 ）传到 store 的有效载荷。它是 store 数据的**唯一**来源。一般来说你会通过 `store.dispatch()` 将 action 传到 store
- Action 本质上是 JavaScript 普通对象。我们约定，action 内必须使用一个字符串类型的 `type` 字段来表示将要执行的动作。多数情况下，`type` 会被定义成字符串常量。当应用规模越来越大时，建议使用单独的模块或文件来存放 action

#### 2.2 Reducer
- **只要传入参数相同，返回计算得到的下一个 state 就一定相同。没有特殊情况、没有副作用，没有 API 请求、没有变量修改，单纯执行计算**
- 最后，时刻谨记永远不要在克隆 `state` 前修改它
- `combineReducers()` 所做的只是生成一个函数，这个函数来调用你的一系列 reducer，每个 reducer **根据它们的 key 来筛选出 state 中的一部分数据并处理**，然后这个生成的函数再将所有 reducer 的结果合并成一个大的对象

#### 2.3 Store

- **Store** 就是把它们联系到一起的对象。Store 有以下职责：
  *   维持应用的 state；
  *   提供`getState()` 方法获取 state；
  *   提供`dispatch(action)`方法更新 state；
  *   通过`subscribe(listener)` 注册监听器;
  *   通过`subscribe(listener)` 返回的函数注销监听器

- 再次强调一下 **Redux 应用只有一个单一的 store**。当需要拆分数据处理逻辑时，你应该使用reducer 组合而不是创建多个 store

- 根据已有的 reducer 来创建 store 是非常容易的.我们使用 `combineReducers()` 将多个 reducer 合并成为一个。现在我们将其导入，并传递 `createStore()`

- `createStore()` 的第二个参数是可选的, 用于设置 state 初始状态。这对开发同构应用时非常有用，服务器端 redux 应用的 state 结构可以与客户端保持一致, 那么客户端可以将从网络接收到的服务端 state 直接用于本地数据初始化
- 注意 subscribe() 返回一个函数用来注销监听器

#### 2.4 数据流
- **严格的单向数据流**是 Redux 架构的设计核心
- Redux 应用中数据的生命周期遵循下面 4 个步骤
  - **1. 调用** `store.dispatch(action)`
    - Action 就是一个描述“发生了什么”的普通对象
    - 你可以在任何地方调用`store.dispatch(action)`，包括组件中、XHR 回调中、甚至定时器中
    
 - **2. Redux store 调用传入的 reducer 函数**
   - Store 会把两个参数传入reducer： 当前的 state 树和 action
   - 注意 reducer 是纯函数。它仅仅用于计算下一个 state。它应该是完全可预测的：多次传入相同的输入必须产生相同的输出。它不应做有副作用的操作，如 API 调用或路由跳转。这些应该在 dispatch action 前发生

 - **3. 根 reducer 应该把多个子 reducer 输出合并成一个单一的 state 树** 
 - **4. Redux store 保存了根 reducer 返回的完整 state 树**


#### 2.5  搭配 React
- 这里需要再强调一下：Redux 和 React 之间没有关系。Redux 支持 React、Angular、Ember、jQuery 甚至纯 JavaScript
- Redux 默认并不包含 React 绑定库，需要单独安装
- Redux 的 React 绑定库是基于**容器组件**和**展示组件**相分离 的开发思想
- 创建一些容器组件把这些展示组件和 Redux 关联起来
- 技术上讲，容器组件就是使用 store.subscribe() 从 Redux state 树中读取部分数据，并通过 props 来把这些数据提供给要渲染的组件
- 你可以手工来开发容器组件，但建议使用使用 React Redux 库的 connect() 方法来生成，这个方法做了性能优化来避免很多不必要的重复渲染。（这样你就不必为了性能而手动实现 React 性能优化建议 中的 shouldComponentUpdate 方法
- 使用 `connect()` 前，需要先定义 `mapStateToProps` 这个函数来指定如何把当前 Redux store state 映射到展示组件的 props 中
- 除了读取 state，容器组件还能分发 action。类似的方式，可以定义 `mapDispatchToProps()` 方法接收 `dispatch()`方法并返回期望注入到展示组件的 props 中的回调方法

- 所有容器组件都可以访问 Redux store，所以可以手动监听它。一种方式是把它以 props 的形式传入到所有容器组件中。但这太麻烦了，因为必须要用 `store` 把展示组件包裹一层，仅仅是因为恰好在组件树中渲染了一个容器组件
- 建议的方式是使用指定的 React Redux 组件 `<Provider>`来 [魔法般的 让所有容器组件都可以访问 store，而不必显示地传递它。只需要在渲染根组件时使用即可


