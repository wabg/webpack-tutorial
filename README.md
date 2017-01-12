关于Webpack的学习

# 安装

1.Node.js包含一个包管理器npm,webpack能通过npm安装：
$ npm install webpack -g(全局安装)

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
    
# 运行

1、添加一个配置文件webpack.config.js；一个入口js文件main.js；一个静态页面 index.html 见demo01

2、运行命令

```bash
$ webpack-dev-server 
//这个可以使用 http://localhost:8080 来预览
```

# 使用

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

8、jQuery/jslite加载

jQuery是一个快速、简洁的JavaScript框架,封装JavaScript常用的功能代码，提供一种简便的JavaScript设计模式，优化HTML

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
