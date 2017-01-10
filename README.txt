Webpack
一、安装
1.Node.js包含一个包管理器npm,webpack能通过npm安装：
$ npm install webpack -g(全局安装)

2.本地安装  为npm添加一个package.json配置文件：$ npm init
安装和添加webpack到 package.json：
$ npm install webpack --save-dev
二、运行
1、添加一个配置文件webpack.config.js；一个入口js文件main.js；一个静态页面 index.html

2、运行命令 $ webpack-dev-server 这个可以使用 http://localhost:8080 来预览

三、使用
1、css加载 Webpack允许你在js文件中引入CSS文件，然后用 CSS-loader 对CSS文件进行预处理，这个例子demo03依赖CSS-loader 和 style-loader。 安装依赖
 npm install css-loader style-loader --save

2、图片加载需要依赖 file-loader 和 url-loader ，安装依赖
npm install url-loader file-loader --save