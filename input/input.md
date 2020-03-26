# 输入框插件使用
```
<apple-input v-model="a" :placeholder="'你好'" :show-word-limit="true" maxlength="10"/>
```

#### 属性
```
v-model // 绑定的值
placeholder // 提示元素input的属性
show-word-limit // 是否显示输入的字数
maxlength // 能过输入最大的字数（仅在show-word-limit为true时生效）
```