### redux-tutorial
[英文原版地址](https://github.com/happypoulp/redux-tutorial)
[中文翻译地址](https://github.com/react-guide/redux-tutorial-cn#redux-tutorial)

---
### 00. introduction
>略

---
### 01. simple-action-creator
- action creator 就是函数而已
- 在后面的章节中，我们会发现 action creator 实际上可以返回 action 以外的其他东西，比如一个函数。 这在处理异步时很有用（更多的内容可以查阅 dispatch-async-action.js
- 为了分发 action，我们需要...一个分发函数
- 并且，为了让任何对它感兴趣的人都能感知到 action 发起，我们还需要一个注册“处理器（handlers）”的机制

---
### 02. about-state-and-meet-redux
- Reducer 函数是 action 的订阅者
- Reducer 函数只是一个纯函数，它接收应用程序的当前状态以及发生的 action，然后返回修改后的新状态
- 如何把数据变更传播到整个应用程序——使用订阅者来监听状态的变更情况。
- 总之 Redux 提供了：
  - 1）存放应用程序状态的容器
  - 2）一种把 action 分发到状态修改器的机制，也就是 reducer 函数
  - 3）监听状态变化的机制

创建一个store
```js
import { createStore } from 'redux'
    var store = createStore(fn);
```
>注意createStore 函数必须接收一个能够修改应用状态的函数，否则报错

---
### 03. simple-reducer
- 在创建一个 Redux 实例前（createStore前），需要给它一个 reducer 函数
- 往 createStore 传 Reducer 的过程就是给 Redux 绑定 action 处理函数（也就是 Reducer）的过程
- 在被调用时，一个 reducer 会得到这些参数：(state, action)
- 在应用初始化时，Redux dispatch 了一个初始化的 action `({ type: '@@redux/INIT' })`
- 在应用初始化时，state 还没被初始化，因此它的值是 "undefined"

---
### 04. get-state
- 小结一下：调用  reducer ，只是为了响应一个派发来的 action

---
### 05. combine-reducers
- Redux 不关心我们到底是只有一个 reducer ，还是有一打（12个）reducer
- 如果我们有多个 reducer ，Redux 能帮我们合并成一个
- 在这种多个 reducer 的模式下，我们可以让每个 reducer 只处理整个应用的部分 state 
- 但我们需要知道，createStore 只接收一个 reducer 函数
- 那么，我们怎么合并所有的 reducer？ 我们又该如何告诉 Redux 每个 reducer 只处理一部分 state 呢.其实这很简单。我们使用 combineReducers 辅助函数
- combineReducers 接收一个对象并返回一个函数，当 combineReducers 被调用时，它会去调用每个reducer，并把返回的每一块 state 重新组合成一个大 state 对象（也就是 Redux 中的 Store）

---
### 06. dispatch-action
- 用一个 action creator 去发送一个 action
- 如果我们要在 dispatch action 之前做一些异步的操作，那应该怎么做呢
- 至止，我们接触的应用流程是这样的：` ActionCreator -> Action -> dispatcher -> reducer`

---
### 07. dispatch-async-action
>略

---
### 08. dispatch-async-action-2
- 使用自定义中间件（middleware）来支持异步 action

---
### 09. middleware
- 为了让 Redux 知道我们有一个或多个中间件，我们使用 Redux 的辅助函数：applyMiddleware.

---
### 10. state-subscriber
- 使用 “provide” 和 “connect” 绑定，不必再关心隐含在内的订阅方法

---
### 11. Provider-and-connect
>略

---
###  12. final-words
>略
