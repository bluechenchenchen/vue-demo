<script>
function noop() {}
export default {
  props: {
    panes: Array,
    currentName: String,
    onTabClick: {
      type: Function,
      default: noop
    }
  },
  methods: {},
  render() {
    const { panes, currentName, onTabClick } = this;
    return (
      <div class="tabs-navs flex">
        {panes &&
          panes.map(item => {
            return (
              <div
                class={
                  currentName === item.name ? "nav-item is-active" : "nav-item"
                }
                onClick={ev => {
                  onTabClick(ev, item.name);
                }}
              >
                <a>{item.label}</a>
              </div>
            );
          })}
      </div>
    );
  }
};
</script>

<style lang="scss" scoped>
.flex {
  display: flex;
}
.tabs-navs {
  margin-bottom: 15px;
  border-bottom: 1px solid #ddd;
}
.nav-item {
  margin: 0 20px;
  line-height: 30px;
  &.is-active {
    a {
      color: blue;
      &::after {
        content: "";
        width: 100%;
        height: 1px;
        background: blue;
        position: absolute;
        bottom: 0;
        left: 0;
      }
    }
  }
  a {
    display: block;
    line-height: 30px;
    position: relative;
  }
  &:hover {
    cursor: pointer;
    color: blue;
  }
}
</style>
