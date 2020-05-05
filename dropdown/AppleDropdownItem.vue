<template>
  <li class="apple-dropdown-item" @click="handleClick">
    <slot></slot>
  </li>
</template>

<script>
export default {
  name: "AppleDropdownItem",
  props: {
    command: String
  },
  mounted() {
    this.selectLabel();
  },
  methods: {
    selectLabel() {
      var parent = this.$parent;
      while (parent) {
        if (parent.$options.componentName !== "AppleDropdown") {
          parent = parent.$parent;
        } else {
          this._checkLabel = parent;
          return;
        }
      }
    },
    handleClick() {
      this._checkLabel.isShow = false;
      this._checkLabel.$emit("command", this.command)
    }
  }
};
</script>

<style lang="scss" scoped>
.apple-dropdown-item {
  padding: 5px 15px;
  font-size: 14px;
  cursor: pointer;
  &:hover {
    background-color: #ecf5ff;
    color: #66b1ff;
  }
  &:first-of-type {
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
  }
  &:last-of-type {
    border-bottom-left-radius: 5px;
    border-bottom-right-radius: 5px;
  }
}
</style>