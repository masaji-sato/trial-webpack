# css-loaderをためしてみる

参考：
https://webpack.github.io/docs/stylesheets.html

## style-loader

ヘッダーにstyle要素を埋め込んでくれるみたい

https://github.com/webpack-contrib/style-loader

## css-loader

https://github.com/webpack-contrib/css-loader
https://webpack.js.org/guides/code-splitting-css/


## インストール

```
npm install style-loader css-loader --save-dev
```

### stylesheetとmain.jsとindex.html

スタイルシート

``` stylesheet.css
h1 {
  color: #F00;
}
```

js

``` main.js
require("./stylesheet.css")
```
html

```
<!DOCTYPE html>
<html>
<head></head>
<body>
  <h1>test</h1>
  <script type="text/javascript" src="./dist/bundle.js"></script>
</body>
</html>
```

### ビルド

webpack.config.js

``` javascript
var path = require('path');

module.exports =  {
  entry: './src/main.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    loaders: [{
      test: /\.css$/,
      loader: "style-loader!css-loader"
    }]
  }
}
```

``` javascript
  "scripts": {
    "build": "webpack"
  }
```

```
npm run build
```

### index.htmlを確認

header要素にstyle要素が動的に出力されていることを確認。



## 参考ページ
### css-modules
https://github.com/css-modules/css-modules
http://glenmaddern.com/articles/css-modules

###
http://qiita.com/_likr/items/c335dec5221024ad56bc