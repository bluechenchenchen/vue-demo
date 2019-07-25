<template>
  <div id="app">
    <h2>这里是没有异步数据正常的情况</h2>
    <tabs activeName="a">
      <tab-pane label="tab1" name="a">tab1</tab-pane>
      <tab-pane label="tab2" name="b">tab2</tab-pane>
      <tab-pane label="tab3" name="c">tab3</tab-pane>
      <tab-pane label="tab4" name="d">tab4</tab-pane>
    </tabs>

    <hr/>
     <h2>这里异步数据,拿不到异步name的值，点击某个tab又可以了</h2>
     <tabs activeName="a" ref="tabs">
      <tab-pane :label="`tab1:${name}`" name="a">tab1</tab-pane>
      <tab-pane :label="`tab2:${name}`" name="b">tab2</tab-pane>
      <tab-pane :label="`tab3:${name}`" name="c">tab3</tab-pane>
      <tab-pane :label="`tab4:${name}`" name="d">tab4</tab-pane>
    </tabs>

    <p>应该是我写的组件问题，有没有方法能解决呢</p>
  </div>
</template>

<script>

import TabPane from "@/components/tabs/tab-pane"
import Tabs from "@/components/tabs/tabs"
export default {
  name: 'app',
  components: {
    TabPane,
    Tabs
  },
  data() {
    return {
     name: ''
    }
  },
  created() {
    this.setName();
  },
  methods: {
    setName() {
      setTimeout(() => {
        this.name = 'bb'
        this.$refs.tabs.calcPaneInstances();
        // eslint-disable-next-line no-console
        console.log('setTimeout')
      }, 1000)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
