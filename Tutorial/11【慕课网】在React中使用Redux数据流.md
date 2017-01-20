### 在React中使用Redux数据流
[教程地址：在React中使用Redux数据流](http://www.imooc.com/learn/744)

---
### 第1章 在React中使用Redux数据流--课程介绍 
#### 1-1 1 课程介绍
- Redux维护了一个单一的状态树

---
###  第2章 在React中使用Redux数据流--基本概念
#### 2-1 单向数据流
- 介绍了点Flux

#### 2-2 Redux介绍
- 介绍Redux的处理流程

---
###  第3章 在React中使用Redux数据流--react回顾
#### 3-1 React回顾
- 快速回顾一下react

----
###  第4章 介绍react-redux 
#### 4-1 react-redux安装及框架介绍
- 当页面渲染完，UI就出现了，然后用户触发UI上的Action，然后Action被送到Reducer这个方法里去，然后Reducer更新了Store，Store里包含react开发的State，最后State决定UI层的展现。这就是Redux的一个完整过程
- redux是可以以独立的库工作的，可以应用在普通的前端项目里，不是一定要应用在react里

---
###  第5章 学习react-redux
#### 5-1 react-redux项目结构
项目的基本结构
- actions：行为
- components：UI组件
- container：容器组件
- reducer：Store里分发Action的方法
- index.html：模板文件
- server.js
- webpack

#### 5-2 action和reducer
- **action**：1.是行为的抽象；2.是普通JS对象；3.一般由方法生成；4.必须有一个type
- **reducer**:1.是响应的抽象；2.纯方法（非存方法是指比如依赖当前的时间）

#### 5-3 介绍store
- **store**:1.action作用于store；2.reducer根据store响应；3.对于redux来说，store是唯一的；4.store包括了完整的state；5.state完全可预测

#### 5-4 介绍组件
- 组件分为UI组件和容器组件，前者只负责展示，后者负责管理数据和传递数据给UI组件显示

---
###  第6章 开发样例工程
#### 6-1 官方demo项目介绍
>略

#### 6-2 demo项目详解之项目结构
>略

#### 6-3 demo项目详解之action
- 分析用户行为，设置Action Creator

#### 6-4 demo项目详解之reducer1
>略

#### 6-5 demo项目详解之reducer2
>略

#### 6-6 demo项目详解之reducer3
- 使用redux提供的combineReducers方法合并所有的reducer

#### 6-7 demo项目详解之组件1
- ref的一种新写法

#### 6-8 demo项目详解之组件2
- 卡在了`connect(mapStateToProps, mapDispatchToProps)()`

#### 6-9 demo项目详解之组件3
>懵

#### 6-10 0 demo项目详解之入口文件包装
- 在最外层包装了一个react-redux提供的Provider组件，将store当成props传递进去，被Provider包在内部的各级组件都能访问到store,其实现原理其实是用了react的context

---
###  第7章 在React中使用Redux数据流--扩展知识 
#### 7-1 扩展知识
- react-redux: redux对react的绑定
- redux-thunk: 实现异步action
- redux-gen: 利用生成器去实现middleware
- react-router-redux: 路由
- react-redux-form: 表单提交

---
###  第8章 在React中使用Redux数据流--课程小结 
####8-1 课程小结
>略

