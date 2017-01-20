### Redux 入门教程（一）：基本用法
[教程地址;Redux 入门教程（一）：基本用法](http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_one_basic_usages.html)

---
### 零、你可能不需要 Redux
- 首先明确一点，Redux 是一个有用的架构，但不是非用不可。事实上，大多数情况，你可以不用它，只用 React 就够了
- 如果你不知道是否需要 Redux，那就是不需要它
- 只有遇到 React 实在解决不了的问题，你才需要 Redux
- 简单说，如果你的UI层非常简单，没有很多互动，Redux 就是不必要的，用了反而增加复杂性

---
### 一、预备知识
- Redux 有很好的[文档](http://redux.js.org/)，还有配套的小视频（[前30集](https://egghead.io/courses/getting-started-with-redux)，[后30集](https://egghead.io/courses/building-react-applications-with-idiomatic-redux)）。你可以先阅读本文，再去官方材料详细研究

---
### 二、设计思想
- Redux 的设计思想很简单，就两句话
  - Web 应用是一个状态机，视图与状态是一一对应的
  - 所有的状态，保存在一个对象里面

---
### 三、基本概念和 API

#### 3.1 Store
- Store 就是保存数据的地方，你可以把它看成一个容器。整个应用只能有一个 Store
- Redux 提供`createStore`这个函数，用来生成 Store
- `createStore`函数接受另一个函数作为参数，返回新生成的 Store 对象

#### 3.2 State
- `Store`对象包含所有数据。如果想得到某个时点的数据，就要对 Store 生成快照。这种时点的数据集合，就叫做 State
- 当前时刻的 State，可以通过`store.getState()`拿到
- Redux 规定， 一个 State 对应一个 View。只要 State 相同，View 就相同。你知道 State，就知道 View 是什么样，反之亦然

#### 3.3 Action
- State 的变化，会导致 View 的变化。但是，用户接触不到 State，只能接触到 View。所以，State 的变化必须是 View 导致的。Action 就是 View 发出的通知，表示 State 应该要发生变化了
- Action 是一个对象。其中的`type`属性是必须的，表示 Action 的名称。其他属性可以自由设置
- 改变 State 的唯一办法，就是使用 Action。它会运送数据到 Store

#### 3.4 Action Creator
- View 要发送多少种消息，就会有多少种 Action。如果都手写，会很麻烦。可以定义一个函数来生成 Action，这个函数就叫 Action Creator

#### 3.5 store.dispatch()
- `store.dispatch()`是 View 发出 Action 的唯一方法

#### 3.6 Reducer
- Store 收到 Action 以后，必须给出一个新的 State，这样 View 才会发生变化。这种 State 的计算过程就叫做 Reducer
- Reducer 是一个函数，它接受 Action 和当前 State 作为参数，返回一个新的 State

#### 3.7 纯函数
- Reducer 函数最重要的特征是，它是一个纯函数。也就是说，只要是同样的输入，必定得到同样的输出
- 纯函数是函数式编程的概念，必须遵守以下一些约束
  *   不得改写参数
  *   不能调用系统 I/O 的API
  *   不能调用`Date.now()`或者`Math.random()`等不纯的方法，因为每次会得到不一样的结果

- 由于 Reducer 是纯函数，就可以保证同样的State，必定得到同样的 View。但也正因为这一点，Reducer 函数里面不能改变 State，必须返回一个全新的对象
- 最好把 State 对象设成只读。你没法改变它，要得到新的 State，唯一办法就是生成一个新对象

#### 3.8 store.subscribe()
- Store 允许使用`store.subscribe`方法设置监听函数，一旦 State 发生变化，就自动执行这个函数
- 显然，只要把 View 的更新函数（对于 React 项目，就是组件的`render`方法或`setState`方法）放入`listen`，就会实现 View 的自动渲染
- `store.subscribe`方法返回一个函数，调用这个函数就可以解除监听

---
### 四、Store 的实现
- 上一节介绍了 Redux 涉及的基本概念，可以发现 Store 提供了三个方法
  *   store.getState()
  *   store.dispatch()
  *   store.subscribe()

- `createStore`方法还可以接受第二个参数，表示 State 的最初状态。这通常是服务器给出的

---
### 五、Reducer 的拆分
- Reducer 函数负责生成 State。由于整个应用只有一个 State 对象，包含所有数据，对于大型应用来说，这个 State 必然十分庞大，导致 Reducer 函数也十分庞大
- Redux 提供了一个`combineReducers`方法，用于 Reducer 的拆分。你只要定义各个子 Reducer 函数，然后用这个方法，将它们合成一个大的 Reducer
- 这种写法有一个前提，就是 State 的属性名必须与子 Reducer 同名。如果不同名，就要采用下面的写法
- 总之，`combineReducers()`做的就是产生一个整体的 Reducer 函数。该函数根据 State 的 key 去执行相应的子 Reducer，并将返回结果合并成一个大的 State 对象

---
### 六、工作流程
- 首先，用户发出 Action
- 然后，Store 自动调用 Reducer，并且传入两个参数：当前 State 和收到的 Action。 Reducer 会返回新的 State
- State 一旦有变化，Store 就会调用监听函数
- `listener`可以通过`store.getState()`得到当前状态。如果使用的是 React，这时可以触发重新渲染 View

---
### 七、实例：计数器
- [github: redux](https://github.com/reactjs/redux)
- [Redux Counter Example](https://github.com/reactjs/redux/tree/master/examples/counter)
