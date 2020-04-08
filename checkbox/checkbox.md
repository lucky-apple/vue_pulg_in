# 多选框插件使用

#### 使用方式一
```
<apple-checkbox label="asda" v-model="check"></apple-checkbox>
data() {
	return {
	  check: true,
	};
},
```

#### 使用方式二
```
<apple-checkbox-group v-model="check1">
      <apple-checkbox label="a"></apple-checkbox>
      <apple-checkbox label="b"></apple-checkbox>
      <apple-checkbox label="c"></apple-checkbox>
</apple-checkbox-group>
data() {
	return {
	  check1:["a", "b", "c"]
	};
},
```

#### 属性介绍
```
v-model 类型Array/Boolean
label 类型 String 显示的字
disabled 类型 Boolean 是否禁用
indeterminate 类型 Boolean 样式控制
change 事件 参数改变的值
```