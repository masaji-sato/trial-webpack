# babel loaderを使ってjsをトランスフォームしてみる

## main.jsにletをつかって変数宣言

```
let test = 5;
```

## babel-loaderを使用せずにバンドルしてみる

以下の設定をつかってバンドルして、出力されたbundle.js内を確認し、letが変換されていないことを確認。

```
var path = require('path');

module.exports =  {
  entry: './main.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  }
}
```

## babel-loaderを使用してバンドルしてみる

参考ページ
https://webpack.github.io/docs/usage.html

### babelとpresetをインストール
```
npm install --save-dev babel-core babel-preset-es2015
```

### babel-loaderをインストール
```
npm install --save-dev babel-loader
```

### jsをトランスフォームするためのpresetを、.babelrcファイル内に設定
```
 { "presets": [ "es2015" ] }
```

### バンドル

webpack設定ファイル。

node_modulesディレクトリ意外のjsファイルをbabel-loaderを使ってトランスフォームする。

.babelrcでpresetを設定済みであることもポイント。

```
var path = require('path');

module.exports =  {
  entry: './main.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module: {
    loaders: [{
      test: /\.js$/,
      exclude: /node_modules/,
      loader: 'babel-loader'
    }]
  }
}
```

package.jsonのscripts

```
"scripts": {
  "build": "webpack"
}
```
ビルドの実行
```
npm run build
```

bundle.jsを確認して、main.jsで記述したletがvarに変換されていることを確認。






