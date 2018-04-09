# vue-upload-ie8

兼容ie8+的文件上传组件，使用jquery、jquery.form插件。

引入jquery：
```js
/* 下载插件 */
npm i jquery jquery-form --save

/* webpack.base.conf.js */
const webpack = require('webpack')

module.exports = {
  ...
  plugins: [
    new webpack.ProvidePlugin({
      $: 'jquery',
      jQuery: 'jquery'
    })
  ]
}

/* upload.vue中引入 */
import $ from 'jquery'
import 'jquery-form'
```

打包报错：
```js
/* config/index.js */
module.exports = {
  ...
  build: {
    assetsPublicPath: ''
  }
}
```

后台服务是[node-upload](https://github.com/nsnds/node-upload)项目
