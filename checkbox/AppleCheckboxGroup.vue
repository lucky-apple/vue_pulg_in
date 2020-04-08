<template>
  <div class="apple_checkbox-group">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "AppleCheckboxGroup",
  componentName: "AppleCheckboxGroup",
  props: {
    disabled: Boolean,
    min: Number,
    value: {}
  },
  watch: {
    value(val) {
    //   console.log(val);
    }
  },
  data() {
    return {};
  }
};
</script>