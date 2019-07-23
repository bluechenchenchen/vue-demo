<docs>

</docs>
<script>
import TabNav from "./tab-nav";
export default {
  components: {
    TabNav
  },
  props: {
    activeName: String
  },
  data() {
    return {
      currentName: this.activeName
    };
  },
  methods: {
    handleTabClick(ev, tabName) {
      this.currentName = tabName;
      this.$emit("tab-click", tabName, ev);
    },
    calcPaneInstances() {
      if (this.$slots.default) {
        const panes = this.$slots.default.map(item => {
          return {
            label:
             item.componentOptions.propsData.label ||item.data.attrs.label,
            name:item.componentOptions.propsData.name ||item.data.attrs.name
          };
        });
        this.panes = panes;
      }
    }
  },
  render() {
    let { panes, currentName, handleTabClick } = this;
    const navData = {
      props: {
        panes,
        currentName,
        onTabClick: handleTabClick
      }
    };
    return (
      <div class="tabs-container tabs">
        <tab-nav {...navData} />
        <div class="tabs-panels">{this.$slots.default}</div>
      </div>
    );
  },
  created() {
    this.calcPaneInstances();
    // eslint-disable-next-line no-console
    console.log('created')
  },
  mounted() {
    this.calcPaneInstances();
    // eslint-disable-next-line no-console
    console.log('mounted')
  },
  updated() {
    this.calcPaneInstances();
    // eslint-disable-next-line no-console
    console.log('updated')
  }
};
</script>

<style lang="scss" scoped></style>
