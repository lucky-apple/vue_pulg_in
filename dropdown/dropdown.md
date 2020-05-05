# 下拉菜单插件使用
```
<apple-dropdown trigger="click" @command="handleCommand">
  <span class="apple-dropdown-label">下拉菜单</span>
  <apple-dropdown-menu slot="dropdown">
	<apple-dropdown-item command="a">第一</apple-dropdown-item>
	<apple-dropdown-item command="b">第二</apple-dropdown-item>
	<apple-dropdown-item command="c">第三</apple-dropdown-item>
  </apple-dropdown-menu>
</apple-dropdown>

 methods: {
	handleCommand(e) {
		console.log(e) // 输出apple-dropdown-item的command值
	}
}
```

### 配置参数
```
trigger 类型String 默认值hover 可选值：click/hover
@command 事件item点击事件 参数item的command
```

### apple-dropdown插槽
```
默认插槽
dropdown 
```

### apple-dropdown-menu插槽
```
默认插槽
```

### apple-dropdown-item插槽
```
默认插槽
```