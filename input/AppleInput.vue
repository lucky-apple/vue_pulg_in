<template>
  <div class="apple-input">
    <div class="apple-input_group">
      <input
        ref="input"
        class="input"
        v-bind="$attrs"
        @input="handleInput"
        :placeholder="placeholder"
        @compositionend="handleCompositionEnd"
      />
      <span class="show-text" v-if="showWordLimit">{{textLength}}/{{upperLimit}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppleInput",
  props: {
    placeholder: {
      type: String,
      default: () => ""
    },
    showWordLimit: {
      type: Boolean,
      default: () => true
    }
  },
  data() {
    return {
      textLength: 0,
    };
  },
  computed: {
    upperLimit() {
      return this.$attrs.maxlength
    }
  },
  methods: {
    handleCompositionEnd(event) {
      this.handleInput(event)
    },
    handleInput(event) {
      this.textLength = event.target.value.length
      this.$emit("input", event.target.value);
    }
  }
};
</script>

<style lang="scss" scoped>
.apple-input {
  display: inline;
  .apple-input_group {
    display: inline-block;
    position: relative;
    .show-text {
      position: absolute;
      right: 5px;
      bottom: 5px;
    }
    .input {
      cursor: pointer;
      height: 40px;
      border: 1px solid #ccc;
      border-radius: 5px;
      padding-left: 20px;
      font-size: 16px;
    }
    .input:focus {
      outline: none;
      border-color: #409eff;
    }
  }
}
</style>