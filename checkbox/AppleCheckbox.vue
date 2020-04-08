<template>
  <label class="check_box" :class="[
    {'is-disabled': isDisabled}
  ]">
    <!-- <span class="ap_check-inner is-indeterminate is-disabled"></span> -->
    <span
      class="ap_check-inner"
      :class="{
        'ap_checkbox': isCheck,
        'is-indeterminate': isIndeterminate,
        'is_checkbox': isCheck,
        'is-disabled': isDisabled
      }"
    ></span>
    <input
      class="ap_check_inp"
      type="checkbox"
      v-model="model"
      :disabled="isDisabled"
      :value="label"
      @change="handleChange"
    />
    <span>
      <slot></slot>
      {{label}}
    </span>
  </label>
</template>

<script>
export default {
  name: "AppleCheckbox",
  data() {
    return {
      selfModel: false,
      focus: false
    };
  },
  props: {
    disabled: Boolean,
    label: String,
    indeterminate: Boolean,
    value: {}
  },
  computed: {
    isIndeterminate() {
      return this.indeterminate
    },
    isCheck() {
      if ({}.toString.call(this.model) === "[object Boolean]") {
        return this.model;
      } else if (Array.isArray(this.model)) {
        return this.model.indexOf(this.label) > -1;
      }
    },
    isGroup() {
      let parent = this.$parent;
      while (parent) {
        if (parent.$options.componentName !== "AppleCheckboxGroup") {
          parent = parent.$parent;
        } else {
          this._checkboxGroup = parent;
          return true;
        }
      }
      return false;
    },
    isDisabled() {
      return this.disabled;
    },
    defaultCheck() {
      return this.$attrs.value;
    },
    model: {
      get() {
        return this.isGroup
          ? this._checkboxGroup.value
          : this.value !== undefined
          ? this.value
          : this.selfModel;
      },
      set(val) {
        if (this.isGroup) {
          this.$parent.$emit("input", val);
        } else {
          this.$emit("input", val);
          this.selfModel = val;
        }
      }
    }
  },
  methods: {
    handleInput(event) {
      this.$emit("input", event.target.value);
    },
    handleChange(ev) {
      if (this.isGroup) {
        this.$parent.$emit("change", this._checkboxGroup.value);
      } else {
        this.$emit("change", this.value);
      }
    }
  }
};
</script>

<style lang="less" scoped>
.is-disabled {
  color: #c0c4cc;
  cursor: not-allowed;
}
.check_box {
  margin-right: 3vh;
  .ap_check-inner {
    display: inline-block;
    vertical-align: bottom;
    position: relative;
    border: 1px solid #409eff;
    border-radius: 2px;
    box-sizing: border-box;
    width: 15px;
    height: 15px;
    background-color: #fff;
    z-index: 1;
    transition: border-color 0.25s cubic-bezier(0.71, -0.46, 0.29, 1.46),
      background-color 0.25s cubic-bezier(0.71, -0.46, 0.29, 1.46);
  }
  .is-indeterminate:after {
    content: "";
    position: absolute;
    display: block;
    height: 2px;
    transform: scale(0.5);
    left: 0;
    right: 0;
    top: 5px;
  }
  .ap_checkbox,.is-indeterminate {
    background-color: #409eff;
    border-color: #409eff;
  }
  .ap_check_inp {
    height: 0;
    width: 0;
  }
  .ap_checkbox {
    vertical-align: text-bottom;
    display: inline-block;
    height: 15px;
    width: 15px;
    border-radius: 2px;
    position: relative;
  }
  .is_checkbox {
    background-color: #409eff;
    border-color: #409eff;
  }
  .ap_checkbox.is_checkbox:after {
    transform: rotate(45deg) scaleY(1);
  }
  .ap_checkbox:after {
    box-sizing: content-box;
    background: transparent !important;
    content: "";
    border: 1px solid #fff;
    border-left: 0;
    border-top: 0;
    height: 7px;
    left: 5px;
    position: absolute;
    top: 1px;
    transform: rotate(45deg) scaleY(0);
    width: 3px;
    transition: transform 0.15s ease-in 0.05s;
    transform-origin: center;
  }
  .is-disabled:after {
    cursor: not-allowed;
    border-color: #c0c4cc;
  }
  .is-indeterminate.is-disabled:after {
    background: #c0c4cc;
  }
  .is-disabled {
    background-color: #edf2fc;
    border-color: #dcdfe6;
  }
}
</style>