html-yu-plugin
=================== 


Inspired by [HTML-webpack-plugin](https://github.com/ampedandwired/html-webpack-plugin)
  
This is a plugin for webpack based on [HTML-webpack-plugin](https://github.com/ampedandwired/html-webpack-plugin),which enable you to inject js both head and body individually

And what is more,acrodding to our project, i provide a blockFile option,which can directly inject a html code blocks before the closing body tag;


Installation
------------
Install the plugin with npm:
```shell
$ npm install html-yu-plugin --save-dev
```


Basic Usage
-----------

The plugin will generate an HTML5 file for you that includes all your webpack
bundles in the body using `script` tags. Just add the plugin to your webpack
config as follows:

```javascript
var HtmlWebpackPlugin = require('html-yu-plugin')
var webpackConfig = {
  entry: 'index.js',
  output: {
    path: 'dist',
    filename: 'index_bundle.js'
  },
  plugins: [
    new HtmlWebpackPlugin({           
        filename:'/view/index.html',  
        template:'./src/view/index.html', 
        inject:true,  //this value must be true
        heads:['response'],  //place the js which wanna be placed inside head tag
        blockFile:"./src/view/summarize.js" //this file's code will be injected within the body tag;
    })
  ]
}
```

This will generate a file `index.html` like the following:
```html
<!DOCTYPE html>
<html>
  <head>
    <script src="/webpack/dist/js/response.js"></script>
  </head>
  <body>
   <script src="/webpack/dist/js/main.js"></script>
   <script>
   // such as baidu statics code;
    </script>
  </body>
</html>
