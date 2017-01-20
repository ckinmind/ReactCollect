### Babel 入门教程
[教程地址：Babel 入门教程](http://www.ruanyifeng.com/blog/2016/01/babel.html)

---
- Babel是一个广泛使用的转码器，可以将ES6代码转为ES5代码，从而在现有环境执行，这意味着，你可以现在就用ES6编写程序，而不用担心现有环境是否支持

---
### 一、配置文件.babelrc
- Babel的配置文件是`.babelrc`，存放在项目的根目录下。使用Babel的第一步，就是配置这个文件
- 该文件用来设置转码规则和插件，基本格式如下

```
{
  "presets": [],
  "plugins": []
}
```

- presets字段设定转码规则，官方的规则集，可以根据需要安装。

```
# ES2015转码规则
$ npm install --save-dev babel-preset-es2015

# react转码规则
$ npm install --save-dev babel-preset-react

# ES7不同阶段语法提案的转码规则（共有4个阶段），选装一个
$ npm install --save-dev babel-preset-stage-0
$ npm install --save-dev babel-preset-stage-1
$ npm install --save-dev babel-preset-stage-2
$ npm install --save-dev babel-preset-stage-3
```

- 然后，将这些规则加入.babelrc

```
  {
    "presets": [
      "es2015",
      "react",
      "stage-2"
    ],
    "plugins": []
  }
```

---
### 二、命令行转码babel-cli
- Babel提供babel-cli工具，用于命令行转码
- 基本用法如下

```
# 转码结果输出到标准输出
$ babel example.js

# 转码结果写入一个文件
# --out-file 或 -o 参数指定输出文件
$ babel example.js --out-file compiled.js
# 或者
$ babel example.js -o compiled.js

# 整个目录转码
# --out-dir 或 -d 参数指定输出目录
$ babel src --out-dir lib
# 或者
$ babel src -d lib

# -s 参数生成source map文件
$ babel src -d lib -s
```

---
### 三、babel-node
- `babel-cli`工具自带一个`babel-node`命令，提供一个支持ES6的REPL环境。它支持Node的REPL环境的所有功能，而且可以直接运行ES6代码
- 它不用单独安装，而是随`babel-cli`一起安装。然后，执行`babel-node`就进入PEPL环境
- `babel-node`命令可以直接运行ES6脚本


---
### 四、babel-register
- `babel-register`模块改写`require`命令，为它加上一个钩子。此后，每当使用`require`加载`.js`、`.jsx`、`.es`和`.es6`后缀名的文件，就会先用Babel进行转码
- 需要注意的是，`babel-register`只会对`require`命令加载的文件转码，而不会对当前文件转码。另外，由于它是实时转码，所以只适合在开发环境使用

---
### 五、babel-core
- 如果某些代码需要调用Babel的API进行转码，就要使用`babel-core`模块

---
###  六、babel-polyfill
- Babel默认只转换新的JavaScript句法（syntax），而不转换新的API，比如Iterator、Generator、Set、Maps、Proxy、Reflect、Symbol、Promise等全局对象，以及一些定义在全局对象上的方法（比如`Object.assign`）都不会转码
- 举例来说，ES6在`Array`对象上新增了`Array.from`方法。Babel就不会转码这个方法。如果想让这个方法运行，必须使用`babel-polyfill`，为当前环境提供一个垫片

```
npm install --save babel-polyfill

//然后，在脚本头部，加入如下一行代码
import 'babel-polyfill';
// 或者
require('babel-polyfill');
```

---
### 七、浏览器环境
- Babel也可以用于浏览器环境。但是，从Babel 6.0开始，不再直接提供浏览器版本，而是要用构建工具构建出来。如果你没有或不想使用构建工具，可以通过安装5.x版本的babel-core模块获取
- browser.js是Babel提供的转换器脚本，可以在浏览器运行。用户的ES6脚本放在script标签之中，但是要注明type="text/babel"


---
### 八、在线转换
- Babel提供一个REPL在线编译器，可以在线将ES6代码转为ES5代码。转换后的代码，可以直接作为ES5代码插入网页运行

---
### 九、与其他工具的配合
- 许多工具需要Babel进行前置转码，这里举两个例子：ESLint和Mocha
