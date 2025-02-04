<template>
  <DataPanel/>
</template>

<script>

import DataPanel from './components/DataPanel.vue'

export default {
  name: 'App',
  components: {
    DataPanel
  }
}
</script>

<style>
#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50; */
  height: 100vh;
  width: 100%;
  font-family: "微软雅黑";
  color: #fff;
  font-size: 16px;
  background: radial-gradient(90% 90%, #034f8e, #034987, #02366d, #002353);
}

body{
  margin: 0px;
}


</style>
