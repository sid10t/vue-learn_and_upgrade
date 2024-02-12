<template>
  <div id="app">
    <data-parent></data-parent>
  </div>
</template>

<script>
import DataParent from "./components/DataParent.vue";

export default {
  name: "App",
  components: {
    DataParent,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
