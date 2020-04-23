<script>
export default {
  name: "AppleTabNav",
  componentName: "AppleTabNav",
  props: {
    panes: Array
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
    isAction() {
      return this.isTab
        ? this._applePane
          ? this._applePane.value
          : false
        : false;
    }
  },
  methods: {
    handleTabClick(tag) {
      this._applePane.$emit("on-click", tag);
    }
  },
  render(h) {
    const { panes, isAction, handleTabClick } = this;
    let title = this._l(panes, (pane, index) => {
      return (
        <div
          class={{
            "apple-tab_title": true,
            "apple-tabs_action": isAction == pane.name
          }}
          on-click={e => handleTabClick(pane)}
        >
          {pane.label}
        </div>
      );
    });
    return <div class="apple-tab_nav">{title}</div>;
  }
};
</script>

<style lang="scss" scoped>
.apple-tab_nav {
  float: left;
  .apple-tab_title {
    display: inline-block;
    width: 15vh;
    height: 10vh;
    line-height: 10vh;
  }
  .apple-tabs_action {
    background: white;
    border-right: 1px solid #ccc;
    border-left: 1px solid #ccc;
  }
  .apple-tab_title:first-of-type {
    border-left: none;
  }
}
</style>