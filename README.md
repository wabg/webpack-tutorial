关于Webpack的学习
===

本教材适用于超级新手查看和参阅。主要用于学习Webpack构建前端项目，中间穿插着React.js的使用。

# 目录

- [前言](#前言)
  - [Node.js](#nodejs)
  - [NPM](#npm)
  - [Webpack](#webpack)
- [安装](#安装)
  - [初始化配置](#初始化配置)
  - [安装webpack](#安装webpack)
- [实例运行](#实例运行)
- [使用功能介绍](#使用功能介绍)
  - [资源加载](#资源加载)
    - [babel加载](#babel加载)
    - [css加载](#css加载)
    - [CSS Modules](#css-modules-见demo05)
    - [图片加载](#图片加载---见demo04)
  - [UglifyJs插件](#uglifyjs插件-见demo06)
  - [HTML Webpack插件](#html-webpack插件--见demo07)
  - [命令启动打开入口路径](#命令启动打开入口路径----见demo8)
  - [环境变量的使用](#环境变量的使用)
  - [代码分割](#代码分割)
  - [用bundle-loader分割代码](#用bundle-loader分割代码-见demo11)
  - [普通模块React应用](#普通模块react应用---见demo12)
  - [jQuery/jslite加载](#jqueryjslite加载--见demo13)
  - [每个模块中使用JSLite或者jQuery](#每个模块中使用jslite或者jquery-demo14)
  - [暴露全局变量](#暴露全局变量)
  - [模块热替换](#模块热替换hot-module-replacemen)
  - [React Router 配置](#react-router-配置--见demo18)
- [参考资料](#参考资料)

## 前言

下面介绍webpack及与webpack相关的几个软件工具的概念。

### Node.js

[Node.js](http://nodejs.org/)  是一个在浏览器外部创建互联网应用程序的框架，它基于 Google 开发的 V8 JavaScript 引擎，轻量，高效，事件驱动，非阻塞I/O，特别适合运行于跨分布式设备的实时数据处理程序。

**作用**

1. 搭建web网络应用
1. 开发Unix命令行工具
1. 开发构建工具，辅助前端开发(webpack,grunt,gulp..)

**优点**

1. 采用事件驱动、异步编程，为网络服务而设计。
2. Node.js非阻塞模式的IO处理给Node.js带来在相对低系统资源耗用下的高性能与出众的负载能力。
3. Node.js轻量高效，可以认为是数据密集型分布式部署环境下的实时应用系统的完美解决方案。
4. Node非常适合如下情况：在响应客户端之前，您预计可能有很高的流量，但所需的服务器端逻辑和处理不一定很多。

**缺点**

1. 可靠性低，可以使用其它方法来提高可靠性。
2. 单进程，只支持单核CPU，默认不能充分的利用多核CPU服务器，一旦这个进程崩掉，那么整个web服务就崩掉了，可以通过自带的方法或者pm2管理工具来利用多核CPU。

### NPM

[npm](https://www.npmjs.com/) (node package manager) node.js的包管理器，用于node插件管理（安装、卸载、更新、管理依赖等）。

**是做什么的？**

1. JS开发人员可以轻松地更新、共享和重用代码。
1. 管理项目中的依赖包模块
1. 与他人分享和接收反馈

**替代工具**

1. **cnpm**：淘宝网提供的国内NPM镜像，因为npm安装插件是从外国服务器下载，受网络影响大，可能出现异常。 
1. **yarn**：是Facebook、Google、Exponent 和 Tilde 联合推出了一个新的 JS 包管理工具，是为了弥补 npm 的安装包（packages）的速度不够快、拉取的 packages 可能版本不同、npm 允许在安装 packages 时执行代码可能产生安全隐患等一些缺陷而出现的


### Webpack

[Webpack](http://webpack.github.io/)它是一个模块打包器，我们将他用于前端项目流程构建，能通过npm安装，还可以使用`cnpm`、`yarn`等工具安装，下面介绍npm安装

**可以做哪些事儿？**

1. 使用loader转换器将各种类型的资源转换成 JavaScript 模块来进行处理
1. 代码压缩、分割、合并
1. 打包静态资源
1. 自动生成HTML5离线缓存配置等....

可以使用功能远不止于此，Webpack有强大的社区，维护着许多插件，这些插件可以帮助你自动化构建您的项目。

**同类工具**

1. `grunt`：是基于Node.js的项目构建工具。它可以自动运行你所设定的任务。Grunt拥有数量庞大的插件,几乎任何你所要做的事情都可以用Grunt实现。
1. `gulp`：基于Node.js实现 Web 前端自动化开发的工具，能够自动化处理你在做项目以后需要完成的一系列的重复工作。比如，压缩代码，合并代码，检查语法是否正确，优化图片等等你可以需要手动重复处理的事情，利用它能够极大的提高开发效率。


## 安装

首先要安装[Node.js](https://nodejs.org/en/download/)， Node.js 自带了软件包管理器 npm,用 npm 安装 Webpack

### 初始化配置

在安装之前需要初始化一个`package.json`

```bash
$ npm init
```

**注**：每个项目的根目录下面，一般都有一个项目配置文件package.json，定义了这个项目所需要的各种模块，以及项目的配置信息（比如名称、版本、许可证等元数据）。npm install命令根据这个配置文件，自动下载所需的模块，也就是配置项目所需的运行和开发环境。
关于package.json [详见package.json](http://javascript.ruanyifeng.com/nodejs/packagejson.html)

### 安装webpack

```shell
# 方法一
$ npm install webpack -g        # 全局安装

# 方法二
$ npm install webpack --save    # 本地安装，存储到配置（package.json）中
```


**本地安装**，工具独立于每个项目，比如一些项目依赖`webpack 1.0` 一些项目依赖 `2.0` 这时可使用本地安装来构建项目。

`--save` 通过这个参数，将保存配置信息至package.json（package.json是nodejs项目配置文件）  
`--save-dev ` 保存至package.json的devDependencies节点，不指定-dev将保存至dependencies节点  

**全局安装**，适用于新手初学，只做一个项目，或者做实例演示。

`-g` 在安装工具的时候添加这个参数，即可安装到全局。  

本地安装使用 `npm install webpack --save` 时package.json文件中的依赖项`dependencies`会添加一行依赖，代码如下：

```json
"dependencies": {
    "webpack": "^1.14.0"
}
```

本地安装，会将依赖包安装到，跟package.json同级目录下的 `node_modules` 目录。这些依赖工具通过 `require()` 或者 ES6 语法调用工具。

如果想要安装指定版本，使用命令如下：

```shell
$ npm install webpack@2.2.0-rc.3
```
    
本项目在写的时候使用的是，webpack beta版本，没有正式发布。在运行的过程中，相应的其它的工具也需要配置新版本，下面是我的配置仅提供参考：

```json
"dependencies": {
    "webpack": "~2.2.0-rc.3",
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
    
## 实例运行

添加一个配置文件webpack.config.js；一个入口js文件main.js；一个静态页面 index.html 见[demo01](./demo01)

### 实例代码

index.html

```html
<!DOCTYPE html>
<html>
<head>
	<title>webpack demo01</title>
</head>
<body>
	<script type="text/javascript" src="boudle.js"></script>
</body>
</html>
```

main.js

```js
document.write('<h1>hello world</h1>');
```

webpack.config.js

```js
module.exports = {
	entry: './main.js',
	output:{
		filename: 'boudle.js'

	}
};
```

### 运行命令

```bash
$ webpack
//会生成一个bundle.js文件 

$ webpack-dev-server 
//访问http://localhost:8080/，你可以在浏览器中看到"hello world"
```

## 使用功能介绍


### 资源加载

Webpack 本身只能处理 JavaScript 模块，如果要处理其他类型的文件，就需要使用   loader 进行转换。详见 http://webpackdoc.com/loader.html

#### Babel加载 

加载预处理插件，可将 JSX/ES6 转换成 js 文件。见[demo02](./demo02)

index.html

```html
<!DOCTYPE html>
<html>
<head>
	
	<title>webpack demo02</title>
</head>
<body>
	<div id="wrapper"></div>
	<script type="text/javascript" src="bundle.js"></script>
	
</body>
</html>
```

main.jsx

```jsx
const React = require('react');
const ReactDOM = require('react-dom');

ReactDOM.render(
    <h1>Hello, world!</h1>,
    document.querySelector('#wrapper')
);
```

webpack.config.js

```js
module.exports = {    
    entry: './main.jsx',
    output: {
        filename: 'bundle.js'
    },
    module: {
        // loaders:[
        //     {
        //       test: /\.js[x]?$/,
        //       exclude: /node_modules/,
        //       loader: 'babel-loader?presets[]=es2015&presets[]=react'
        //     },
        // ]
        loaders: [
            {
                test: /\.jsx?$/,
                exclude: /node_modules/,
                loader: 'babel',   //.jsx文件使用babel处理
                query: {
                    presets: ['es2015', 'react']
                }
            }
        ]
    }
};
```

安装依赖  

```js
npm install babel-loader babel-preset-es2015 babel-preset-react react react-dom --save
```

#### css加载 

Webpack允许你在js文件中引入CSS文件，然后用 CSS-loader 对CSS文件进行预处理，这个例子[demo03](./demo03)依赖CSS-loader 和 style-loader。

index.html

```html
<!DOCTYPE html>
<html>
<head>
	
	<script type="text/javascript" src="bundle.js"></script>
</head>
<body>

	<h1>hello world</h1>
</body>
</html>
```

main.js

```js
require('./app.css');
```

webpack.config.js

```js
module.exports = {
    entry: './main.js',
    output: {
        filename: 'bundle.js'
    },
    module: {
        loaders:[
            { test: /\.css$/, loader: 'style-loader!css-loader' }, //.css 文件使用 style-loader 和 css-loader 来处理
        ]
    }
};
```
app.css

```js
body {
   color: #000;
  background: #fff;
  margin: 0;
  padding: 0;
  font-family: Georgia, Palatino, serif;
}
```

安装依赖

```bash
 npm install css-loader style-loader --save
```

#### CSS Modules 见[demo05](./demo05)
CSS Modules 不是将 CSS 改造成编程语言，只是加入了局部作用域和模块依赖，这恰恰是网页组件最急需的功能。

**局部作用域**

CSS的规则都是全局的，任何一个组件的样式规则，都对整个页面有效。产生局部作用域的唯一方法，就是使用一个独一无二的class的名字，不会与其他选择器重名。这就是 CSS Modules 的做法。

**全局作用域**

CSS Modules 允许使用:global(.className)的语法，声明一个全局规则。凡是这样声明的class，都不会被编译成哈希字符串。


index.html

```js<html>
<body>
	<h1 class="h1">hello world</h1>
	<h2 class="h2">hello webpack</h2>
	<div id="example"></div>
	<script src="./bundle.js"></script>
</body>
</html>
```

main.jsx

```js
var React = require('react');
var ReactDOM = require('react-dom');
var style = require('./app.css');

ReactDOM.render(
  <div>
    <h1 className={style.h1}>Hello World</h1>
    <h2 className="h2">Hello Webpack</h2>
  </div>,
  document.getElementById('example')
);
```

app.css

```css
.h1{color: red;}
:global(.h2){color: blue;}
```

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
            },{
                test: /\.css$/,
                loader: 'style-loader!css-loader?modules'
            }
        ]
    }
};
```


#### 图片加载   见[demo04](./demo04)

需要依赖 file-loader 和 url-loader，两个都必须用上，否则超过大小限制的图片无法生成到目标文件夹中

index.html

```js
<!DOCTYPE html>
    <body>
        <script type="text/javascript" src="bundle.js"></script>
    </body>
</html>
```

main.js

```js
var img1 = document.createElement("img");
img1.src = require("./small.png");
document.body.appendChild(img1);

var img2 = document.createElement("img");
img2.src = require("./big.png");
document.body.appendChild(img2);
```

webpack.config.js

```js
module.exports = {
    entry: './main.js',
    output: {
        filename:'bundle.js'
    },
    module:{
        loaders:[
            { test: /\.(png|jpg)$/, loader: 'url-loader?limit=8192'} //图片文件使用 url-loader 来处理，小于8kb的直接转为base64
        ]
    }
}
```

安装依赖

```bash
npm install url-loader file-loader --save
```


### UglifyJs插件 见[demo06](./demo06)

Webpack 有插件系统来扩展其功能。例如：UglifyJs Plugin将 main.js 压缩，输出压缩版本的bundle.js。但加入了这个插件之后，编译的速度会明显变慢，所以一般只在生产环境启用。 

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

### HTML Webpack插件  见[demo07](./demo07)

html-webpack-plugin 能创建index.html 文件

main.js

```js
document.write('<h1>Hello World</h1>');
```
webpack.config.js

```js
var HtmlwebpackPlugin = require('html-webpack-plugin');
module.exports = {
    entry: './main.js',
    output: {
        filename: 'bundle.js'
    },
    plugins: [
        new HtmlwebpackPlugin({
          title: 'Webpack-demos'
        })
    ]
};
```

### 命令启动打开入口路径    见[demo8](./demo08)

open-browser-webpack-plugin可以自动打开http://localhost:8080/，把demo07稍做更改，在webpack.config.js中的 module.exports.plugins 添加一个插件。

webpack.config.js

```js
plugins: [
    new HtmlwebpackPlugin({
      title: 'Webpack-demos'
    }),
    new OpenBrowserPlugin({
      url: 'http://localhost:8080'
    })
]
```

### 环境变量的使用 

定义一个环境变量__DEV__，通过环境变量来运行webpack-dev-server 命令。只有在开发环境中使用环境变量，才能使某些代码起作用。

main.js

```js
document.write('<h1>Hello World</h1>');

if (__DEV__) {
  document.write(new Date());//当环境变量__DEV__为真时，输出日期
}
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
var devFlagPlugin = new webpack.DefinePlugin({
    __DEV__: JSON.stringify(JSON.parse(process.env.DEBUG || 'false'))//定义环境变量
});

module.exports = {
    entry: './main.js',
    output: {
      filename: 'bundle.js'
    },
    plugins: [devFlagPlugin]
};
```

通过环境变量来运行webpack-dev-server 命令

```bash
# Linux & Mac
$ env DEBUG=true webpack-dev-server

# Windows
$ DEBUG=true webpack-dev-server
```

### 代码分割

webpack 可以把你的代码拆分到“chunks”里面去，从而让你的代码可以按需加载，这样就可以保证初始文件加载变小，在应用需要的时候在加载需要的模块。

这个非常重要，构建大型应用的时候，你需要将你的代码分模块，不然你的js越来越大，加载速度越来越慢，分块也适合项目模块化，多人共同应用开发。

我们在下面的例子[demo10](./demo10) 用的是CommonJs 的加载方式 require.ensure 你可以到[官网](http://webpack.github.io/docs/code-splitting.html)看更多的模块加载方式 

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

### 用bundle-loader分割代码 见[demo11](./demo11)

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

index.html

```html
<!DOCTYPE html>
<html>
<body>
	<script src="bundle.js"></script>
</body>
</html>
```
webpack.config.js

```js
module.exports = {
	entry:'./main.js',
	output:{
		filename: 'bundle.js'

	}
};
```

运行 webpack 命令之后就生成两个js 文件 bundle.js 和 1.bundle.js ，页面 index.html 引用入口文件 bundle.js 。


### 普通模块React应用   见[demo12](./demo12)

React是一个用于构建可组合的用户界面的库，是现在最热门的前端框架。[了解 React](https://facebook.github.io/react/blog/2013/06/05/why-react.html) 与 [学习 React](http://www.ruanyifeng.com/blog/2015/03/react.html)

下面通过使用commonschunkplugin插件来演示React的应用 

当多个脚本有共同的部分，可以使用commonschunkplugin提取公共部分为一个单独的.js文件。
此方法的好处是:
在加载多个文件时，它们的公共部分只加载一次；
缩小打包文件体积，实现项目优化

不使用commonschunkplugin时

main.js

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
    <script src="bundle1.js"></script>
    <script src="bundle2.js"></script>
  </body>
</html>
```

webpack.config.js

```js
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
    }
}
```

webpack运行之后可以看到

```bash
Hash: ad3b4921919e04babc7b
Version: webpack 1.14.0
Time: 3074ms
     Asset    Size  Chunks             Chunk Names
bundle1.js  740 kB       0  [emitted]  bundle1
bundle2.js  740 kB       1  [emitted]  bundle2
    + 179 hidden modules
```

使用commonschunkplugin

main.js

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

运行之后发现

```bash
Hash: d1811c6827b2519f4bd7
Version: webpack 1.14.0
Time: 2958ms
     Asset       Size  Chunks             Chunk Names
bundle1.js  298 bytes       0  [emitted]  bundle1
bundle2.js  300 bytes       1  [emitted]  bundle2
   init.js     742 kB       2  [emitted]  init.js
    + 179 hidden modules
```


### jQuery/jslite加载  见[demo13](./demo13)

jQuery是一个快速、简洁的JavaScript框架,封装JavaScript常用的功能代码，提供一种简便的JavaScript设计模式，优化HTML。

安装依赖

```bash
$ npm install jquery --save
```

相应的main.js写成

```js
var $ = require('jslite');
$('h1').text('Hello World');//相当于<h1>hello world<h2>

```
### 每个模块中使用JSLite或者jQuery [demo14](./demo14)

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

### 暴露全局变量

[demo15](./demo15)可以在 webpack.config.js 中使用 externals。

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

### 模块热替换（Hot Module Replacemen）

这个工具的作用：在交换、添加或删除模块时，应用程序继续运行而无需重新加载页面。

现在有两种方法让webpack服务端模块热更换。

1、使用webpack命令的两个子命令

```bash
$ webpack-dev-server --hot --inline
//--hot: 加HotModuleReplacementPlugin切换服务器热加载模式。
--inline: 嵌入运行的webpack-dev-server中。
--hot --inline: 添加一个指向 webpack/hot/dev-server.
```

2、修改webpack配置文件---webpack.config.js

将`new webpack.HotModuleReplacementPlugin()`添加到plugins中。

将'webpack/hot/dev-server' 和 'webpack-dev-server/client?http://localhost:8080'添加到 entry

修改如下：

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

不要关闭服务器,将App.js的'Hello World'改成'Hello Webpack'，保存后看看浏览器的变化。见[demo17](./demo17)


### React Router 配置  见[demo18](./demo18)
 * Router 与 Route 一样都是 react 组件 ，它的 history 对象是整个路由系统的核心，它暴漏了很多属性和方法在路由系统中使用；
 * Redirect 是一个重定向组件，有 from 和 to 两个属性；
 * browserHistory ：是由 React Router 创建浏览器应用推荐的 history。它使用 History API 在浏览器中被创建用于处理 URL，新建一个像这样真实的 URL example.com/some/path。
 * hashHistory ：这是一个你会获取到的默认 history ，如果你不指定某个 history 。它用到的是 URL 中的 hash（#）部分去创建形如 example.com/#/some/path 的路由，支持 ie8＋ 的浏览器，但是因为是 hash 值，所以不推荐使用。
 * createMemoryHistory ：不会在地址栏被操作或读取。

index.html

 ```html
 <html>
  <body>
    <div id="app"></div>
    <script src="/bundle.js"></script>
  </body>
</htmL>
```
app.css

```css
header *{
  display: inline;
  margin: 1em;
  border-bottom: 1px solid black;
}
```
index.js

```js
import React from 'react';
import { render } from 'react-dom';
import { Router, Route, Link, IndexRoute, browserHistory } from 'react-router';

require('./app.css');

var App = React.createClass({
  render: function () {
    return (
      <div>
        <header>
          <ul>
            <li><Link to="/app">Dashboard</Link></li>
            <li><Link to="/inbox">Inbox</Link></li>
            <li><Link to="/calendar">Calendar</Link></li>
          </ul>
          Logged in as Jane
        </header>
        {this.props.children}
      </div>
    );
  }
});

var Dashboard = React.createClass({
  render: function () {
    return (
      <div>
        <p>Dashboard</p>
      </div>
    );
  }
});

var Inbox = React.createClass({
  render: function () {
    return (
      <div>
        <p>Inbox</p>
      </div>
    );
  }
});

var Calendar = React.createClass({
  render: function () {
    return (
      <div>
        <p>Calendar</p>
      </div>
    );
  }
});

render((
  <Router history={browserHistory}>
    <Route path="/" component={App}>
      <IndexRoute component={Dashboard}/>
      <Route path="app" component={Dashboard}/>
      <Route path="inbox" component={Inbox}/>
      <Route path="calendar" component={Calendar}/>
      <Route path="*" component={Dashboard}/>
    </Route>
  </Router>
), document.querySelector('#app'));
```

webpack.config.js

```js
module.exports = {
  entry: './index.js',
  output: {
    filename: 'bundle.js'
  },
  module: {
    loaders:[
      { test: /\.css$/, loader: 'style-loader!css-loader' },
      { test: /\.js[x]?$/, exclude: /node_modules/, loader: 'babel-loader?presets[]=es2015&presets[]=react' },
    ]
  }
};
```

## 参考资料

- [ruanyf/webpack-demos ](https://github.com/ruanyf/webpack-demos)
- [package.json](http://javascript.ruanyifeng.com/nodejs/packagejson.html)
- [Node.js 概述](http://javascript.ruanyifeng.com/nodejs/basic.html)
- [React入门实例教程](http://www.ruanyifeng.com/blog/2015/03/react.html) 
