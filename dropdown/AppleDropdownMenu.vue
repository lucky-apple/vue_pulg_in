<template>
  <transition name="el-zoom-in-top">
    <ul class="apple-dropdown-menu" v-show="isShow">
      <slot></slot>
    </ul>
  </transition>
</template>

<script>
export default {
  name: "AppleDropdownMenu",
  componentName: "AppleDropdownMenu",
  computed: {
    isShow() {
      this.selectLabel();
      return !this._checkLabel ? false : this._checkLabel.isShow;
    }
  },
  mounted() {
    document.body.appendChild(this.$el);
    // this.selectLabel();
    if (this._checkLabel) {
      var el = this._checkLabel.$el,
        left = el.offsetLeft,
        buttom = el.offsetTop;
      this.$el.style.top = buttom + "px";
      this.$el.style.left = left + "px";
      this._checkLabel.initEvent();
    }
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
    }
  }
};
</script>

<style lang="scss" scoped>
.el-zoom-in-top-enter-active, .el-zoom-in-top-leave-active {
  transition: opacity .5s;
}
.el-zoom-in-top-enter, .el-zoom-in-top-leave-to /* .fade-leave-active below version 2.1.8 */ {
   opacity: 0;
}
.apple-dropdown-menu {
  list-style: none;
  position: absolute;
  background: white;
  border-radius: 5px;
  padding: 0;
  margin-top: 20px;
  border: 1px solid #ebeef5;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
}
</style>