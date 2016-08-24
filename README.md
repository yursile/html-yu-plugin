html-yu-plugin
=================== 


Inspired by [HTML-webpack-plugin](https://github.com/ampedandwired/html-webpack-plugin)
  
This is a plugin for webpack based on HTML-webpack-plugin,which will enable you to inject js both head and body individually

And what is more,to meet the need of our project, I provide blockFile and headBlockFile option,which can directly inject some html code blocks after the start body tag and before the closing body tag

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
        blockFile:"./src/view/statistics.html", //this file's code will be injected within the body tag;
        headBlockFile:"./src/view/loading.html"  //prepend to the body
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
    <!-- the loading block is injected  -->
    <div class="loading">
      <div class="pace"></div>
    </div>
    <script src="/webpack/dist/js/main.js"></script>


    <!-- here also can be injected with some stuff like statistics  -->
    <script type="text/javascript">
      // such as baidu statistics code;
    </script>
  </body>
</html>
