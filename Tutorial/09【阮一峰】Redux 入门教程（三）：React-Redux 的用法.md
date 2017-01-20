
### Redux 入门教程（三）：React-Redux 的用法
[教程地址：Redux 入门教程（三）：React-Redux 的用法](http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_three_react-redux.html)

---
- 为了方便使用，Redux 的作者封装了一个 React 专用的库 [React-Redux](https://github.com/reactjs/react-redux)
- 这个库是可以选用的。实际项目中，你应该权衡一下，是直接使用 Redux，还是使用 React-Redux。后者虽然提供了便利，但是需要掌握额外的 API，并且要遵守它的组件拆分规范


---
###  一、UI 组件
- React-Redux 将所有组件分成两大类：UI 组件（presentational component）和容器组件（container component）
- UI 组件有以下几个特征
  *   只负责 UI 的呈现，不带有任何业务逻辑
  *   没有状态（即不使用`this.state`这个变量）
  *   所有数据都由参数（`this.props`）提供
  *   不使用任何 Redux 的 API

- 因为不含有状态，UI 组件又称为"纯组件"，即它纯函数一样，纯粹由参数决定它的值

---
### 二、容器组件
- 容器组件的特征恰恰相反
  *   负责管理数据和业务逻辑，不负责 UI 的呈现
  *   带有内部状态
  *   使用 Redux 的 API

- 总之，只要记住一句话就可以了：UI 组件负责 UI 的呈现，容器组件负责管理数据和逻辑
- ，如果一个组件既有 UI 又有业务逻辑，那怎么办？回答是，将它拆分成下面的结构：外面是一个容器组件，里面包了一个UI 组件。前者负责与外部的通信，将数据传给后者，由后者渲染出视图
- React-Redux 规定，所有的 UI 组件都由用户提供，容器组件则是由 React-Redux 自动生成。也就是说，用户负责视觉层，状态管理则是全部交给它

---
### 三、connect()
- React-Redux 提供`connect`方法，用于从 UI 组件生成容器组件。`connect`的意思，就是将这两种组件连起来
- `connect`方法接受两个参数：`mapStateToProps`和`mapDispatchToProps`。它们定义了 UI 组件的业务逻辑。前者负责输入逻辑，即将`state`映射到 UI 组件的参数（`props`），后者负责输出逻辑，即将用户对 UI 组件的操作映射成 Action

---
### 四、mapStateToProps()
- `mapStateToProps`是一个函数。它的作用就是像它的名字那样，建立一个从（外部的）`state`对象到（UI 组件的）`props`对象的映射关系
- 作为函数，`mapStateToProps`执行后应该返回一个对象，里面的每一个键值对就是一个映射
- `mapStateToProps`会订阅 Store，每当`state`更新的时候，就会自动执行，重新计算 UI 组件的参数，从而触发 UI 组件的重新渲染
- `mapStateToProps`的第一个参数总是`state`对象，还可以使用第二个参数，代表容器组件的`props`对象

---
### 五、mapDispatchToProps()
- `mapDispatchToProps`是`connect`函数的第二个参数，用来建立 UI 组件的参数到`store.dispatch`方法的映射。也就是说，它定义了哪些用户的操作应该当作 Action，传给 Store。它可以是一个函数，也可以是一个对象

---
### 六、`<Provider>` 组件
- `connect`方法生成容器组件以后，需要让容器组件拿到`state`对象，才能生成 UI 组件的参数
- 一种解决方法是将`state`对象作为参数，传入容器组件。但是，这样做比较麻烦，尤其是容器组件可能在很深的层级，一级级将`state`传下去就很麻烦
- React-Redux 提供`Provider`组件，可以让容器组件拿到`state`
- `Provider`在根组件外面包了一层，这样一来，里面的所有子组件就默认都可以拿到`state`了
- 它的原理是`React`组件的[`context`](https://facebook.github.io/react/docs/context.html)属性

---
### 七、实例：计数器
- 完整的代码看[这里](https://github.com/jackielii/simplest-redux-example/blob/master/index.js)

---
### 八、React-Router 路由库
- 使用`React-Router`的项目，与其他项目没有不同之处，也是使用`Provider`在`Router`外面包一层，毕竟`Provider`的唯一功能就是传入`store`对象
- [一个react-redux的demo](https://github.com/cag2050/react_redux_demo161019)
