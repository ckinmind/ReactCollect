### Redux 简明教程
[教程地址：Redux 简明教程](https://github.com/kenberkeley/redux-simple-tutorial)

---
### 1. 为什么要用 Redux
比如有如下需求
- 需求 1：在控制台上记录用户的每个动作
- 需求 2：在上述需求的基础上，记录用户的操作时间
- ...

---
### 2. Store
- state 是应用的状态，一般本质上是一个普通对象
- store 是应用状态 state 的管理者，包含下列四个函数
  *   `getState() # 获取整个 state`
  *   `dispatch(action) # ※ 触发 state 改变的【唯一途径】※`
  *   `subscribe(listener) # 您可以理解成是 DOM 中的 addEventListener`
  *   `replaceReducer(nextReducer) # 一般在 Webpack Code-Splitting 按需加载的时候用`

- 二者的关系是：`state = store.getState()`
- Redux 规定，一个应用只应有一个单一的 `store`，其管理着唯一的应用状态 `state`,Redux 还规定，不能直接修改应用的状态 `state`
- 若要改变 `state`，必须 `dispatch` 一个 `action`，这是修改应用状态的不二法门
- 上面提到，`state` 是通过 `store.getState()` 获取，那么 `store` 又是怎么来的呢？想生成一个 `store`，我们需要调用 Redux 的 `createStore`

---
### 3. Action
- 上面提到，`action`（动作）实质上是包含 `type` 属性的普通对象，这个 `type` 是我们实现用户行为追踪的关键
- 刨根问底，`action` 是谁生成的呢

---
### 4.  Action Creator
- Action Creator 可以是同步的，也可以是异步的
- 顾名思义，Action Creator 是 `action` 的创造者，本质上就是一个**函数**，返回值是一个 `action`（**对象**）

---
### 5. Reducer
- Reducer 必须是同步的纯函数
- 用户每次 `dispatch(action)` 后，都会触发 `reducer` 的执行
- `reducer` 的实质是一个**函数**，根据 `action.type` 来**更新** `state` 并返回 `nextState`
- 最后会用 `reducer` 的返回值 `nextState` **完全替换掉**原来的 `state`
- 注意：上面的这个 “更新” 并不是指 `reducer` 可以直接对 `state` 进行修改, Redux 规定，须先复制一份 `state`，在副本 `nextState` 上进行修改操作
- 通俗点讲，就是 `reducer` 返回啥，`state` 就被替换成啥

---
### 6. 总结
*   `store` 由 Redux 的 `createStore(reducer)` 生成
*   `state` 通过 `store.getState()` 获取，本质上一般是一个存储着整个应用状态的**对象**
*   `action` 本质上是一个包含 `type` 属性的普通**对象**，由 Action Creator (**函数**) 产生
*   改变 `state` 必须 `dispatch` 一个 `action`
*   `reducer` 本质上是根据 `action.type` 来更新 `state` 并返回 `nextState` 的**函数**
*   `reducer` 必须返回值，否则 `nextState` 即为 `undefined`
*   实际上，**`state` 就是所有 `reducer` 返回值的汇总**（本教程只有一个 `reducer`，主要是应用场景比较简单）

- Action Creator => `action` => `store.dispatch(action)` => `reducer(state, action)` => ~~`原 state`~~ `state = nextState`

---
### 7. 最简单的例子
- [简单的在线演示例子](http://jsbin.com/zivare/edit?html,console)
- 备注：Redux 除了和 React 一起用外，还支持其它界面库，是可以单独使用的，不一定要和react一起使用
