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
### 1. 介绍

#### 1.1 动机
- JavaScript 需要管理比任何时候都要多的 state （状态）
- 复杂性很大程度上来自于：我们总是将两个难以理清的概念混淆在一起：变化和异步
- 美中不足的是，React 依旧把处理 state 中数据的问题留给了你。Redux就是为了帮你解决这个问题
- Redux 试图让 state 的变化变得可预测。这些限制条件反映在 Redux 的三大原则中

#### 1.2 核心概念
- 强制使用 action 来描述所有变化带来的好处是可以清晰地知道应用中到底发生了什么
- action 就像是描述发生了什么的面包屑
- 为了把 action 和 state 串起来，开发一些函数，这就是 reducer
- reducer 只是一个接收 state 和 action，并返回新的 state 的函数

#### 1.3 三大原则
- Redux 可以用这三个基本原则来描述
  - 单一数据源
  - State 是只读的
  - 使用纯函数来执行修改
- 整个应用的 state 被储存在一棵 object tree 中，并且这个 object tree 只存在于唯一一个 store 中
- 惟一改变 state 的方法就是触发 action，action 是一个用于描述**已发生事件**的普通对象
- 为了描述 action 如何改变 state tree ，你需要编写 reducers

#### 1.4 先前技术
- 和 Flux 一样，Redux 规定，将模型的更新逻辑全部集中于一个特定的层（Flux 里的 store，Redux 里的 reducer）
- Flux 和 Redux 都不允许程序直接修改数据，而是用一个叫作 “action” 的普通对象来对更改进行描述
- 虽然出于性能方面的考虑，写不纯的 reducer 来变动数据在技术上是可行的，但我们并不鼓励这么做

#### 1.5 生态系统
- 很多有用的资料

#### 1.6 示例
>略（文档看完后再测试）
