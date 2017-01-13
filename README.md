# 关于Webpack的学习

## 前言

> NPM是一个NodeJS包管理和分发工具，使用可以很快的找到特定服务要使用的包，进行下载、安装以及管理已经安装的包。比如使用 npm 命令安装模块$ npm install <Module Name>

> Webpack 是一个模块打包器，其作用有：

> 首先Webpack 本身能处理原生的 JavaScript 模块；

> 可以使用loader转换器将各种类型的资源转换成 JavaScript 模块，从而任何资源都可以成为 Webpack 可以处理的模块；

> 能够进行代码分割；

> Webpack 有一个功能丰富的插件系统，大多数内容功能都是基于这个插件系统运行的；

> Webpack 还有一个智能解析器，几乎可以处理任何第三方库，无论它们的模块形式是 CommonJS、 AMD 还是普通的 JS 文件。甚至在加载依赖的时候，允许使用动态表达式 require("./templates/" + name + ".jade")。

## 安装

1.Node.js包含一个包管理器npm,webpack能通过npm安装：

```bash
$ npm install webpack -g
//全局安装
```

2.本地安装  
（1）为npm添加一个package.json配置文件：

```bash
$ npm init
# package.json文件可以手工编写，也可以使用npm init命令自动生成
```

（2）添加webpack到 package.json：`$ npm install webpack --save`

```js
//此时package.json文件中会出现如下代码：  
"dependencies": {
    "webpack": "^1.14.0"
//dependencies - 依赖包列表。如果依赖包没有安装，npm 会自动将依赖包安装在 node_module 目录下。
}
  
```

注：1.每个项目的根目录下面，一般都有一个package.json文件，定义了这个项目所需要的各种模块，以及项目的配置信息（比如名称、版本、许可证等元数据）。npm install命令根据这个配置文件，自动下载所需的模块，也就是配置项目所需的运行和开发环境。
关于package.json详见http://javascript.ruanyifeng.com/nodejs/packagejson.html

2.如果想要安装新版本，可在package.json中进行如下配置：
    
```js
  "dependencies": {
    "webpack": "^2.2.0-rc.3"
  }
 ```
  
相应的其他配置改为

```js
"dependencies": {
    "babel-core": "^6.21.0",
    "babel-loader": "^6.2.10",
    "babel-plugin-transform-runtime": "^6.15.0",
    "babel-polyfill": "^6.20.0",
    "babel-preset-babili": "0.0.9",
    "babel-preset-es2015": "^6.18.0",
    "babel-preset-react": "^6.16.0",
    "babel-preset-stage-2": "^6.18.0",
    "babili-webpack-plugin": "0.0.7",
    "html-webpack-plugin": "^2.25.0",
    "moment": "^2.17.1",
    "react": "^15.4.1",
    "react-dom": "^15.4.1"
}
```
    
## 运行

1、添加一个配置文件webpack.config.js；一个入口js文件main.js；一个静态页面 index.html 见[demo01](http://git.showgold.cn/yaojuan/webpack/tree/master/demo01)

2、运行命令

```bash
$ webpack
```

会生成 bundle.js


```bash
$ webpack-dev-server 
//访问http://localhost:8080/index.html，你可以在浏览器中看到"hello world"
```

## 使用

#### Webpack 本身只能处理 JavaScript 模块，如果要处理其他类型的文件，就需要使用   loader 进行转换。详见 http://webpackdoc.com/loader.html

1、Babel加载 加载预处理插件，可将 JSX/ES6 转换成 js 文件。/见[demo02](http://git.showgold.cn/yaojuan/webpack/tree/master/demo02)
安装依赖  

```js
npm install babel-loader babel-preset-es2015 babel-preset-react react react-dom --save

```


2、css加载 Webpack允许你在js文件中引入CSS文件，然后用 CSS-loader 对CSS文件进行预处理，这个例子[demo03](http://git.showgold.cn/yaojuan/webpack/tree/master/demo03)依赖CSS-loader 和 style-loader。 安装依赖

```js
 npm install css-loader style-loader --save
```


3、图片加载需要依赖 file-loader 和 url-loader ，安装依赖

```js
npm install url-loader file-loader --save
//见[demo04](http://git.showgold.cn/yaojuan/webpack/tree/master/demo04)
```

4、css-loader?modules (查询模块的参数) 使用CSS模块的规格。加载CSS模块默认是本地作用域，如果你要将CSS作用于全局，你得将选择器放入global中如:global(.h2) 见[demo05](http://git.showgold.cn/yaojuan/webpack/tree/master/demo05)

5、UglifyJs插件 Webpack 有插件系统来扩展其功能。例如：UglifyJs Plugin将 main.js 输出压缩版本的 bundle.js 见[demo06](http://git.showgold.cn/yaojuan/webpack/tree/master/demo06)

main.js

```js
var longVariableName = 'Hello';
longVariableName += ' World';
document.write('<h1>' + longVariableName + '</h1>');
```

index.html

```html
<html>
<body>
  <script src="bundle.js"></script>
</body>
</html>
```

webpack.config.js

```js
var webpack = require('webpack');
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

运行之后这三个js文件将被压缩成一个文件

```html
<html>
<head></head>
<body>
    <script src="bundle.js"></script>
    <h1>Hello World</h1>
</body>
</html>
//在运行界面右键检查可以查看
//更多内容参见http://rapheal.sinaapp.com/2014/05/22/uglifyjs-squeeze/
```

6、HTML Webpack插件 html-webpack-plugin 能创建index.html 文件。见[demo07](http://git.showgold.cn/yaojuan/webpack/tree/master/demo07)

7、open-browser-webpack-plugin可以自动打开http://localhost:8080/

```js
plugins: [
    new HtmlwebpackPlugin({
      title: 'Webpack-demos'
    }),
    new OpenBrowserPlugin({
      url: 'http://localhost:8080'
    })
]//见[demo8](http://git.showgold.cn/yaojuan/webpack/tree/master/demo08)
```

8、代码分割

webpack 可以把你的代码拆分到“chunks”里面去，从而让你的代码可以按需加载，这样就可以保证初始文件加载变小，在应用需要的时候在加载需要的模块。

这个非常重要，构建大型应用的时候，你需要将你的代码分模块，不然你的js越来越大，加载速度越来越慢，分块也适合项目模块化，多人共同应用开发。

我们在下面的例子[demo10](http://git.showgold.cn/yaojuan/webpack/tree/master/demo10) 用的是CommonJs 的加载方式 require.ensure 你可以到官网看跟多的模块加载方式 

main.js

```js
require.ensure(['./a'], function(require) {
    var content = require('./a');
    document.open();
    document.write('<h1>' + content + '</h1>');
    document.close();
});
```

require.ensure 告诉 webpack 去加载分割出来的 a.js 文件

a.js

```js
module.exports = 'Hello World';
```

按照上面的书写方式，webpack知道你的依赖关系，根据这个依赖关系输出js，然后在index.html页面上引用入口 js 文件 main.js。

```html
<html>
  <body>
    <script src="bundle.js"></script>
  </body>
</html>
```

webpack.config.js

```js
module.exports = {
    entry: './main.js',
    output: {
      filename: 'bundle.js'
    }
};
```

9、用bundle-loader分割代码 见[demo11](http://git.showgold.cn/yaojuan/webpack/tree/master/demo11)

安装依赖$ npm install --save bundle-loader

main.js

```js
var load = require('bundle-loader!./a.js');
// 异步等待加载完成会后执行
load(function(file) {
    document.open();
    document.write('<h1>' + file + '</h1>');
    document.close();
});
```

运行 webpack 命令之后就生成两个js 文件 bundle.js 和 1.bundle.js 页面 index.html 引用入口文件 bundle.js 。

10、当多个脚本有共同的部分，可以提取公共部分为一个单独的文件使用commonschunkplugin方法。见[demo12](http://git.showgold.cn/yaojuan/webpack/tree/master/demo12)

此方法的好处是在运行多个文件时，它们的公共部分只运行一次。

```jsx
// main1.jsx
var React = require('react');
var ReactDOM = require('react-dom');

ReactDOM.render(
  <h1>Hello World</h1>,
  document.getElementById('a')
);

// main2.jsx
var React = require('react');
var ReactDOM = require('react-dom');

ReactDOM.render(
  <h2>Hello Webpack</h2>,
  document.getElementById('b')
);
```

index.html

```html
<html>
  <body>
    <div id="a"></div>
    <div id="b"></div>
    <script src="init.js"></script>
    <script src="bundle1.js"></script>
    <script src="bundle2.js"></script>
  </body>
</html>
```

webpack.config.js

```js
var CommonsChunkPlugin = require("webpack/lib/optimize/CommonsChunkPlugin");
module.exports = {
    entry: {
      bundle1: './main1.jsx',
      bundle2: './main2.jsx'
    },
    output: {
      filename: '[name].js'
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
    plugins: [
      new CommonsChunkPlugin('init.js') //将公共部分放在init.js这个文件中
    ]
}
```

11、jQuery/jslite加载

jQuery是一个快速、简洁的JavaScript框架,封装JavaScript常用的功能代码，提供一种简便的JavaScript设计模式，优化HTML。

安装依赖

```bash
$ npm install jquery --save
```

相应的main.js写成

```js
var $ = require('jslite');
$('h1').text('Hello World');//相当于<h1>hello world<h2>
// 见[demo13](http://git.showgold.cn/yaojuan/webpack/tree/master/demo13)
```
12、每个模块中使用JSLite或者jQuery [demo14](http://git.showgold.cn/yaojuan/webpack/tree/master/demo14)

使用 ProvidePlugin 方法可以把一个模块作为一个变量，只有当你使用变量时才会请求相应的模块。可见官方解释//http://webpack.github.io/docs/shimming-modules.html

index.html

```html
<html>
  <body>
    <h1></h1>
    <script src="bundle.js"></script>
  </body>
</html>
```

main.js

```js
$('h1').text('Hello World');
```

webpack.config.js

```js
var webpack = require('webpack');
module.exports = {
    entry: {
      app: './main.js'
    },
    output: {
      filename: 'bundle.js'
    },
    plugins: [
      new webpack.ProvidePlugin({
        $: "jslite",
        JSLite: "jslite",
        "window.JSLite": "jslite"
      })
    ]
};
```

13、暴露全局变量

[demo15](http://git.showgold.cn/yaojuan/webpack/tree/master/demo15)可以在 webpack.config.js 中使用 externals。官方文档

例如我们有一个data.js

```js
var data = 'Hello World';
```
我们将data作为一个全局变量。
webpack.config.js

```js
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
      // require('data') 应用当做一个全局变量引用进来
      'data': 'data'
    }
};
```
现在你可以在你的main.jsx文件中可以把 data 全局变量当一个包引用进来，实际上它是一个全局变量。

```jsx
var data = require('data');
var React = require('react');
var ReactDOM = require('react-dom');

ReactDOM.render(
  <h1>{data}</h1>,
  document.getElementById('title')
);
```

14、模块热替换（Hot Module Replacemen）

作用：在交换、添加或删除模块时，应用程序继续运行而无需重新加载页面。

现在有两种方法让webpack服务端模块热更换。

1、使用webpack命令的两个子命令

```bash
$ webpack-dev-server --hot --inline
//--hot: 加HotModuleReplacementPlugin切换服务器热加载模式。
--inline: 嵌入运行的webpack-dev-server中。
--hot --inline: 添加一个指向 webpack/hot/dev-server.
```

2、修改webpack.config.js

将new webpack.HotModuleReplacementPlugin()添加到plugins中。

将'webpack/hot/dev-server' 和 'webpack-dev-server/client?http://localhost:8080'添加到 entry

即webpack.config.js

```js
var webpack = require('webpack');
var path = require('path');
module.exports = {
    entry: [
        'webpack/hot/dev-server',
        'webpack-dev-server/client?http://localhost:8080',
        './index.js'
    ],
    output: {
        filename: 'bundle.js',
        publicPath: '/static/'
    },
    plugins: [
      new webpack.HotModuleReplacementPlugin()
    ],
    module: {
      loaders: [{
        test: /\.jsx?$/,
        loaders: ['babel-loader?presets[]=es2015&presets[]=react'],
        include: path.join(__dirname, '.')
      }]
    }
};
```

App.js

```js
import React, { Component } from 'react';

export default class App extends Component {
  render() {
    return (
      <h1>Hello World</h1>
    );
  }
}
```

index.js

```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
ReactDOM.render(<App />, document.getElementById('root'));
```

index.html

```html
<html>
  <body>
    <div id='root'></div>
    <script src="/static/bundle.js"></script>
  </body>
</html>
```

运行命令

```bash
$ webpack-dev-server
```

不要关闭服务器,将App.js的'Hello World'改成'Hello Webpack'，保存后看看浏览器的变化

