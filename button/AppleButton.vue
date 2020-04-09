<template>
  <button class="apple_button" :class="[
    type?type:'',
    size?size:''
  ]"
  @click="click">
    <span v-if="$slots.default">
      <slot></slot>
    </span>
  </button>
</template>

<script>
export default {
  name: "AppleButton",
  props: {
    type: {
      type: String,
      default: "default"
    },
    size: String
  },
  methods: {
    click() {
      this.$emit("click")
    }
  }
};
</script>

<style lang="less" scoped>
.apple_button {
  outline: none;
  border: 0px;
  cursor: pointer;
  padding: 15px 30px;
  border-radius: 5px;
  background: white;
}
.apple_button.default {
  border: 1px solid #ccc;
}
.default:hover {
  color: #409eff;
  border-color: #c6e2ff;
  background-color: #ecf5ff;
}
.apple_button.info {
  color: #fff;
  background-color: #909399;
  border-color: #909399;
}
.apple_button.info:hover {
  background: #a6a9ad;
  border-color: #a6a9ad;
  color: #fff;
}
.apple_button.success {
  color: #fff;
  background-color: #67c23a;
  border-color: #67c23a;
}
.apple_button.success:hover {
  background: #85ce61;
  border-color: #85ce61;
  color: #fff;
}
.apple_button.primary {
  color: #fff;
  background-color: #409eff;
  border-color: #409eff;
}
.apple_button.primary:hover {
  background: #66b1ff;
  border-color: #66b1ff;
  color: #fff;
}
.apple_button.warning {
  color: #fff;
  background-color: #e6a23c;
  border-color: #e6a23c;
}
.apple_button.warning:hover {
  background: #ebb563;
  border-color: #ebb563;
  color: #fff;
}
.apple_button.danger {
  color: #fff;
  background-color: #f56c6c;
  border-color: #f56c6c;
}
.apple_button.danger:hover {
  background: #f78989;
  border-color: #f78989;
  color: #fff;
}
</style>