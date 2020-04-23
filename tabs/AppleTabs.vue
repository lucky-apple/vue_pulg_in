<script>
import AppleTabsNav from "./AppleTabNav";

export default {
  name: "AppleTabs",
  componentName: "AppleTabs",
  props: {
    value: {}
  },
  data() {
    return {
      panes: [],
    };
  },
  components: {
    AppleTabsNav
  },
  methods: {
    tabTitle() {
      if (this.$slots.default) {
        const paneSlots = this.$slots.default.filter(
          vnode =>
            vnode.tag &&
            vnode.componentOptions &&
            vnode.componentOptions.Ctor.options.name === "ApplePane"
        );
        const panes = paneSlots.map(
          ({ componentInstance }) => componentInstance
        );
        this.panes = panes;
      }
    }
  },
  mounted() {
    this.tabTitle();
  },
  render(h) {
    const { panes, action } = this;
    const navData = {
      props: {
        panes
      },
      refs: "nav"
    };
    const head = (
      <div class="apple-tab_head">
        <apple-tabs-nav {...navData}></apple-tabs-nav>
      </div>
    );
    const content = (
      <div class={{ "apple-tab_content": true}}>
        {this.$slots.default}
      </div>
    );
    return (
      <div class="apple-tabs">
        <div class="apple-tabs_box">{[head, content]}</div>
      </div>
    );
  }
};
</script>

<style lang="scss" scoped>
$bg-color: #ccc;

.apple-tabs {
  overflow: hidden;
  border: 1px solid $bg-color;
  .apple-tabs_box {
    width: 100%;
  }
  .apple-tab_head {
    overflow: hidden;
    background: #e4e7ed;
  }
  .apple-tabs_box {
    float: left;
  }
  .apple-tab_content {
    padding: 5vh 5vh;
    float: left;
  }
}
</style>