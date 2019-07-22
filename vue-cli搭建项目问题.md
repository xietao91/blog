## 部分引入element-ui配置 `.babelrc` 文件报错处理
<br/>
按照官方文档部分引入element-ui 运行后会报 'Plugin/Preset files are not allowed to export objects, only functions'错误,经过一番查找之后,解决的方法是安装  `@babel/preset-env` ,并修改 `.babelrc` 配置 'presets'为'@babel/preset-env',原值为'es2015'

安装@babel/preset-env
```
yarn add @babel/preset-env -s -D
```

## vue-cli 引入sass 预处理器
<br/>
首先安装 ` node-sass `和 ` sass-loader `

```
yarn add node-sass -s -D
yarn add sass-loader -s -D
```
使用的话直接在`.vue`文件的style标签添加 lang='scss'属性就能使用.如果需要额外配置的话,再在 `vue.config.js`中添加配置
