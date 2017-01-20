### webpack-demos
[教程地址：webpack-demos](https://github.com/ruanyf/webpack-demos#demo01-entry-file-source)

---

webpack 基础命令
```
webpack           for building once for development
webpack -p        压缩混淆脚本
webpack --watch   监听变动并自动打包
webpack -d        生成map映射文件，告知哪些模块被最终打包到哪里了
webpack --colors  for making things pretty
```

### 1. 入口文件
```js
/* webpack.config.js */
module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  }
};
```
>entry: 打包的入口文件（wepack不会处理index.html）
>output.filename: 打包后的文件名字

---
### 2. 多入口文件
```
/* webpack.config.js */
module.exports = {
  entry: {
    bundle1: './main1.js',
    bundle2: './main2.js'
  },
  output: {
    filename: '[name].js'
  }
};
```
>最终将main1.js以及这个文件require的其他文件打包成bundle1.js
>将main2.js以及这个文件require的其他文件打包成bundle2.js

---
### 3. Babel-loader
```
/* webpack.config.js */
module.exports = {
  entry: './main.jsx',
  output: {
    filename: 'bundle.js'
  },
  module: {
    loaders:[
      {
        test: /\.js[x]?$/,
        exclude: /node_modules/,
        loader: 'babel-loader?presets[]=es2015&presets[]=react'
      },
    ]
  }
};
```
>babel-loader能够将JSX/ES6语法转化为ES5
>这里babel-loader还需要两个插件babel-preset-es2015 和 babel-preset-react


---
### 4. CSS-loader
```
/* webpack.config.js */
module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  },
  module: {
    loaders:[
      { test: /\.css$/, loader: 'style-loader!css-loader' },
    ]
  }
};
```
>css-loader用于在js文件中require一个css文件,读取css文件
>style-loader用于将css样式插入到页面中
>两个loader都要，而且执行顺序是由后至前，先css-loader再style-loader

---
### 5. Image loader
```
module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  },
  module: {
    loaders:[
      { test: /\.(png|jpg)$/, loader: 'url-loader?limit=8192' }
    ]
  }
};
```
>url-loader: 这里配置limit=8192意思是如果图片小于8kb则转化为data url

---
### 6. CSS Module 
```
module.exports = {
  entry: './main.jsx',
  output: {
    filename: 'bundle.js'
  },
  module: {
    loaders:[
      {
        test: /\.js[x]?$/,
        exclude: /node_modules/,
        loader: 'babel-loader',
        query: {
          presets: ['es2015', 'react']
        }
      },
      {
        test: /\.css$/,
        loader: 'style-loader!css-loader?modules'
      }
    ]
  }
};
```
>用于css的模块化，是css也有作用域

---
### 7. UglifyJs Plugin
```
ar webpack = require('webpack');
var uglifyJsPlugin = webpack.optimize.UglifyJsPlugin;
module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  },
  plugins: [
    new uglifyJsPlugin({
      compress: {
        warnings: false
      }
    })
  ]
};
```
>用于代码的混淆压缩

---
### 8. HTML Webpack Plugin and Open Browser Webpack Plugin
>html-webpack-plugin能生成一个html文件
>open-browser-webpack-plugin能够自动打开浏览器

---
### 9. Environment flags
>设置一些环境变量，这样方便开发环境调试

---
### 10. Code splitting
>使用require.ensure 实现代码分割，按需加载

---
### 11. Code splitting with bundle-loader
>使用 bundle-loader来进行代码分割按需加载‘

---
### 12. Common chunk
>抽出公共模块

---
### 13. Vendor chunk
>将公共库抽离出来，不要打成一个包，比如jquery

---
### 14. Exposing global variables
>定义一个全局变量，在webpack.config.js中配置，然后使用的使用当作一个模块引入，这时候这个变量实际是全局变量了(有异议，仔细看例子)

```
// webpack.config.js
module.exports = {
  entry: './main.jsx',
  output: {
    filename: 'bundle.js'
  },
  module: {
    loaders:[
      {
        test: /\.js[x]?$/,
        exclude: /node_modules/,
        loader: 'babel-loader',
        query: {
          presets: ['es2015', 'react']
        }
      },
    ]
  },
  externals: {
    // require('data') is external and available
    //  on the global var data
    'data': 'data'
  }
};


// main.jsx
var data = require('data');
var React = require('react');
var ReactDOM = require('react-dom');

ReactDOM.render(
  <h1>{data}</h1>,
  document.body
);
```

---
### 15. Hot Module Replacement
- 两种方式

```
第一种
webpack-dev-server --hot --inline

第二种
entry: [
    'webpack/hot/dev-server',
    'webpack-dev-server/client?http://localhost:8080',
    './index.js'
  ],
```
>自己尝试两种本地都无法热更新


---
### 16.  React router
>一个react router的例子
