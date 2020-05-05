<script>
export default {
  name: "AppleDropdown",
  componentName: "AppleDropdown",
  props: {
    trigger: {
      type: String,
      default: () => "hover"
    }
  },
  data() {
    return {
      isShow: false,
      timeout: null
    };
  },
  mounted() {},
  methods: {
    initEvent() {
      const that = this;
      let trigger = that.trigger,
        el = this.$slots.default[0].elm,
        dropdownEl = this.$slots.dropdown[0].elm;
      if (trigger === "hover") {
        el.addEventListener("mouseenter", that.show);
        el.addEventListener("mouseleave", that.hide);
        dropdownEl.addEventListener("mouseenter", that.show);
        dropdownEl.addEventListener("mouseleave", that.hide);
      } else if (trigger === "click") {
        el.addEventListener("click", that.handleClick);
      }
    },
    handleClick(e) {
      const that = this;
      if (that.isShow) {
        that.isShow = false;
      } else {
        that.isShow = true;
      }
    },
    show() {
      const that = this;
      if (this.timeout) clearTimeout(this.timeout);
      this.timeout = setTimeout(() => {
        that.isShow = true;
      }, 0);
    },
    hide() {
      const that = this;
      if (this.timeout) clearTimeout(this.timeout);
      this.timeout = setTimeout(() => {
        that.isShow = false;
      }, 0);
    }
  },
  render(h) {
    return (
      <div class="apple-dropdown">
        {this.$slots.default} {this.$slots.dropdown}
      </div>
    );
  }
};
</script>

<style lang="scss" scoped>
.apple-dropdown {
  display: inline;
  .apple-dropdown-label {
    cursor: pointer;
    font-size: 14px;
    color: #409eff;
  }
}
</style>