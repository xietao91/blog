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

如果给元素添加 `key` 属性的话，那么 vue 就会强制更新 dom 顺序结构，如下：

```javascript
[
'<div>2</div>',// id:b
'<div>4</div>',// id:d
'<div>1</div>',// id:a
'<div>5</div>',// id:e
'<div>3</div>',// id:c
]
```

由以上可知，**给列表元素添加 `key` 属性，当其依赖元素发生变化后， vue 会强制更新 dom 结构。**

一般来说，除非列表元素结构非常简单或者不会更新，可以不添加 `key` 属性，最大限度的复用现有的 dom 结构。除此之外都推荐给元素添加独一无二的 `key` 属性。因为依赖默认行为至少有一下几个常见的问题：

- 不会触发过渡动画。
- 不会触发组件生命周期钩子函数（当列表元素是组件时）。
- 会造成一些类似表单元素的状态错乱，例如两个通过 `v-if` 控制显隐的 `input` 标签，其 value 就会出现错位。