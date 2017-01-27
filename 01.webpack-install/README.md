# webpackのインストール

詳細は以下
https://webpack.js.org/guides/installation/

## 実際にやってみよう

### プロジェクトの初期化
npm init

### webpackをインストール
npm install webpack --save-dev

### package.jsonに追記

```
"scripts": {
  "start": "webpack --config mywebpack.config.js"
}
```

### mywebpack.config.jsを作成

main.jsエントリーファイルに指定して、distディレクトリにbundle.jsを作成する。

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

bundle.jsが作成されていることを確認。




