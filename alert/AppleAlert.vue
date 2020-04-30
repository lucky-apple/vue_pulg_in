<template>
  <div class="apple-alert" :class="['apple-alert_' + type, 'is-' + theme]">
    <div class="apple-alert_title">
      <span :class="{'is-blob': description}">
        <span v-if="!$slots.title">{{title}}</span>
        <slot v-if="$slots.title" name="title"></slot>
      </span>
      <i v-if="closable">关闭</i>
    </div>
    <div v-if="description || $slots.description" class="apple-alert_description">
      <span v-if="!$slots.description">{{description}}</span>
      <slot v-if="$slots.description" name="description"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppleAlert",
  props: {
    title: String,
    type: {
      type: String,
      default: () => "info"
    },
    closable: Boolean,
    theme: {
      type: String,
      default: () => "light"
    },
    description: String
  }
};
</script>

<style lang="scss" scoped>
.apple-alert {
  padding: 2vh 5vh;
  border-radius: 1vh;
  font-size: 13px;
  &.apple-alert_success.is-light {
    background-color: #f0f9eb;
    color: #67c23a;
  }
  &.apple-alert_info.is-light {
    background-color: #f4f4f5;
    color: #909399;
  }
  &.apple-alert_warning.is-light {
    background-color: #fdf6ec;
    color: #e6a23c;
  }
  &.apple-alert_error.is-light {
    background-color: #fef0f0;
    color: #f56c6c;
  }
  &.apple-alert_success.is-dark {
    background-color: #67c23a;
    color: #fff;
  }
  &.apple-alert_info.is-dark {
    background-color: #909399;
    color: #fff;
  }
  &.apple-alert_warning.is-dark {
    background-color: #e6a23c;
    color: #fff;
  }
  &.apple-alert_error.is-dark {
    background-color: #f56c6c;
    color: #fff;
  }
  .apple-alert_title {
    text-align: left;
  }
  .apple-alert_description {
    text-align: left;
    margin-top: 10px;
  }
  span {
    &.is-blob {
      font-weight: 700;
    }
  }
  i {
    float: right;
  }
}
</style>