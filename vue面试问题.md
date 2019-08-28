### 1 列表组件添加 key 的作用

 vue 不加 `key` 的默认行为在更新列表时会尽量复用原有的 dom ，例如以下代码

```vue
<div id="app">
	<div v-for="item in dataList">{{item}}</div>
</div>
```

```javascript
const vm = new Vue({
    el:'#app',
    data: {
    	dataList:[1,2,3,4,5]
    }
    
});
```

以上的例子 vue 会生成如下的 dom 数组 ：

```js
[
'<div>1</div>',// id:a
'<div>2</div>',// id:b
'<div>3</div>',// id:c
'<div>4</div>',// id:d
'<div>5</div>',// id:e
]
```

如果更新 `dataList`  => `vm.dataList = [2,4,1,5,3]` , 则上述 dom 会变成这样: 

```javascript
[
'<div>2</div>',// id:a
'<div>4</div>',// id:b
'<div>1</div>',// id:c
'<div>5</div>',// id:d
'<div>3</div>',// id:e
]
```

原有的 dom 顺序结构不会变化，只是每个 dom 的 `innnerHTML` 更新了。