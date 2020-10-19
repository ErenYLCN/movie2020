<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" class="logo" style="background: transparent;">
    <Search />
  </div>
</template>

<script>
import Search from './components/Search.vue'


export default {
  name: 'App',
  components: {
    Search,
  },
}
</script>

<style>
body {
  background: linear-gradient(to bottom, #F6F6F6, #f6f6f6);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.logo {
  height: 200px;
  background: transparent;
}
.bg-right {
  background-color: yellow;
  position: fixed;
  top: 0;
  bottom: 0;
  left: 50%;
  right: 0;
  z-index: -1;
}
</style>
