关于webpack的学习

1、首先

添加一个配置文件webpack.config.js；

```js
module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  }
};

一个入口js文件main.js；

```js
document.write('<h1>Hello World</h1>');

一个静态页面 index.html;

```html
<html>
  <body>
    <script type="text/javascript" src="bundle.js"></script>
  </body>
</html>


2、运行命令

$ webpack-dev-server

这个可以使用 http://localhost:8080 来预览

3、css加载 

Webpack允许你在js文件中引入CSS文件，然后用 CSS-loader 对CSS文件进行预处理，这个例子demo03依赖CSS-loader 和 style-loader。

安装依赖npm install css-loader style-loader --save

4、图片加载

需要依赖 file-loader 和 url-loader 

安装依赖npm install url-loader file-loader --save