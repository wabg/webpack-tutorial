# 关于Webpack的学习

## 前言
  NPM是一个NodeJS包管理和分发工具，使用可以很快的找到特定服务要使用的包，进行下载、安装以及管理已经安装的包。比如使用 npm 命令安装模块$ npm install <Module Name>

Webpack 是一个模块打包器，其作用有：

首先Webpack 本身能处理原生的 JavaScript 模块；

可以使用loader转换器将各种类型的资源转换成 JavaScript 模块，从而任何资源都可以成为 Webpack 可以处理的模块；

能够进行代码分割；

Webpack 有一个功能丰富的插件系统，大多数内容功能都是基于这个插件系统运行的；

Webpack 还有一个智能解析器，几乎可以处理任何第三方库，无论它们的模块形式是 CommonJS、 AMD 还是普通的 JS 文件。甚至在加载依赖的时候，允许使用动态表达式 require("./templates/" + name + ".jade")。

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

1、添加一个配置文件webpack.config.js；一个入口js文件main.js；一个静态页面 index.html 见demo01

2、运行命令

```bash
$ webpack-dev-server 
//这个可以使用 http://localhost:8080 来预览
```

## 使用

#### Webpack 本身只能处理 JavaScript 模块，如果要处理其他类型的文件，就需要使用 loader 进行转换。详见 http://webpackdoc.com/loader.html

1、Babel加载 加载预处理插件，可将 JSX/ES6 转换成 js 文件。
安装依赖  

```js
npm install babel-loader babel-preset-es2015 babel-preset-react react react-dom --save
//见demo02
```


2、css加载 Webpack允许你在js文件中引入CSS文件，然后用 CSS-loader 对CSS文件进行预处理，这个例子demo03依赖CSS-loader 和 style-loader。 安装依赖

```js
 npm install css-loader style-loader --save
```


3、图片加载需要依赖 file-loader 和 url-loader ，安装依赖

```js
npm install url-loader file-loader --save
//见demo04
```

4、css-loader?modules (查询模块的参数) 使用CSS模块的规格。加载CSS模块默认是本地作用域，如果你要将CSS作用于全局，你得将选择器放入global中如:global(.h2) 见demo05

5、UglifyJs插件 Webpack 有插件系统来扩展其功能。例如：UglifyJs Plugin将 main.js 输出压缩版本的 bundle.js  见demo06

6、HTML Webpack插件 html-webpack-plugin 能创建index.html 文件。见demo07

7、open-browser-webpack-plugin可以自动打开http://localhost:8080/

```js
plugins: [
    new HtmlwebpackPlugin({
      title: 'Webpack-demos'
    }),
    new OpenBrowserPlugin({
      url: 'http://localhost:8080'
    })
]//见demo8
```

8、代码分割

webpack 可以把你的代码拆分到“chunks”里面去，从而让你的代码可以按需加载，这样就可以保证初始文件加载变小，在应用需要的时候在加载需要的模块。

这个非常重要，构建大型应用的时候，你需要将你的代码分模块，不然你的js越来越大，加载速度越来越慢，分块也适合项目模块化，多人共同应用开发。

我们在下面的例子demo10 用的是CommonJs 的加载方式 require.ensure 你可以到官网看跟多的模块加载方式 

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

9、用bundle-loader分割代码

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

8、jQuery/jslite加载

jQuery是一个快速、简洁的JavaScript框架,封装JavaScript常用的功能代码，提供一种简便的JavaScript设计模式，优化HTML。

安装依赖

```bash
$ npm install jquery --save
```

相应的main.js写成

```js
var $ = require('jslite');
$('h1').text('Hello World');//相当于<h1>hello world<h2>
// 见demo13
```
