# tabs插件的使用

```
<apple-tabs v-model="tabsValue" @on-click="click">
  <apple-pane :name="item.value" v-for="item in obj" :key="item.value" :label="item.name">{{item.name}}</apple-pane>
</apple-tabs>
data() {
	return {
	  tabsValue:"1",
	  obj: [
		{name: "第一", value: "1"},
		{name: "第二", value: "2"},
		{name: "第三", value: "3"},
		{name: "第四", value: "4"}
	  ]
	};
},
```

### 配置参数

```
v-model/value 类型String
name 标签的值 类型String
label标签文字 类型String
@on-click 点击事件 参数改组件的实例
```