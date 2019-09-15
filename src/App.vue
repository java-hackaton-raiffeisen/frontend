<template>
  <div id="app">
    <nav-bar />
    <router-view />
  </div>
</template>
<script>
import NavBar from "./components/NavBar";

export default {
  components: {
    NavBar
  }
};
</script>
<style lang="scss">

#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
