<template>
  <div id="app">
    <Home />
  </div>
</template>

<script>
import Home from "./components/home/home.vue";

export default {
  name: "App",
  components: {
    Home,
  },
};
</script>

<style>
:root {
  height: 100%;
}

#app {
  height: 100vh;
}

html {
  height: 100%;
  width: 100%;
  overflow: hidden;
}

body {
  height: 100%;
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  user-select: none;
}
</style>
