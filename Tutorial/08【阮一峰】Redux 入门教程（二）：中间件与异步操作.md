### Redux 入门教程（二）：中间件与异步操作
[教程地址：Redux 入门教程（二）：中间件与异步操作](http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_two_async_operations.html)

---
- 一个关键问题没有解决：异步操作怎么办？Action 发出以后，Reducer 立即算出 State，这叫做同步；Action 发出以后，过一段时间再执行 Reducer，这就是异步。怎么才能 Reducer 在异步操作结束后自动执行呢？这就要用到新的工具：中间件（middleware）

---
### 一、中间件的概念
- 为了理解中间件，让我们站在框架作者的角度思考问题：如果要添加功能，你会在哪个环节添加
  - （1）Reducer：纯函数，只承担计算 State 的功能，不合适承担其他功能，也承担不了，因为理论上，纯函数不能进行读写操作。
  - （2）View：与 State 一一对应，可以看作 State 的视觉层，也不合适承担其他功能。
  - （3）Action：存放数据的对象，即消息的载体，只能被别人操作，自己不能进行任何操作。

- 中间件就是一个函数，对`store.dispatch`方法进行了改造，在发出 Action 和执行 Reducer 这两步之间，添加了其他功能

---
### 二、中间件的用法
- `createStore`方法可以接受整个应用的初始状态作为参数，那样的话，`applyMiddleware`就是第三个参数了
- 中间件的次序有讲究

---
### 三、applyMiddlewares()
- `applyMiddlewares`这个方法是 Redux 的原生方法，作用是将所有中间件组成一个数组，依次执行

---
### 四、异步操作的基本思路
- 理解了中间件以后，就可以处理异步操作了。同步操作只要发出一种 Action 即可，异步操作的差别是它要发出三种 Action
  *   操作发起时的 Action
  *   操作成功时的 Action
  *   操作失败时的 Action

---
### 五、redux-thunk 中间件
- 暂时看不懂，不止从何整理

---
### 六、redux-promise 中间件
- 既然 Action Creator 可以返回函数，当然也可以返回其他值。另一种异步操作的解决方案，就是让 Action Creator 返回一个 Promise 对象。这就需要使用`redux-promise`中间件
