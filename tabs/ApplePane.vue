<script>
export default {
  name: "ApplePane",
  componentName:"AppleTabs",
  props: {
    name: String,
    label: String
  },
  methods: {
    
  },
  computed: {
    isTab() {
      let $parent = this.$parent;
      while ($parent) {
        if ($parent.$options.componentName !== "AppleTabs") {
          $parent = $parent.$parent;
        } else {
          this._applePane = $parent;
          return true;
        }
      }
      return false;
    },
    isShow() {
      return this.isTab?this._applePane.value == this.name:false;
    }
  },
  render(h) {
    let { isShow } = this;
    const content = ( 
      <span class={{"apple_pane-nav": true}}>
        {this.$slots.default}
      </span>
    );
    return (
      <div class={{"apple_pane": true, "apple-tab_show": isShow }}>
        {content}
      </div>
    );
  }
};
</script>

<style lang="scss" scoped>
.apple_pane {
  display: none;
  .apple_pane-nav.is_action {
    background: blue;
  }
}
.apple_pane.apple-tab_show {
  display: inline-block;
}
</style>