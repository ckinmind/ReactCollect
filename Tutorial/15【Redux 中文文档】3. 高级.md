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
### 3. 高级
- 基础章节介绍了如何组织简单的 Redux 应用。在这一章节中，将要学习如何使用 AJAX 和路由

#### 3.1 异步 Action
