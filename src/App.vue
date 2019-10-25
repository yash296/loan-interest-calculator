<template>
  <v-app id="app">
    <AppBar />
    <v-content>
      <v-card tile style="height:100%; position:fixed; width:100%;overflow-y:auto">
        <router-view />
      </v-card>
    </v-content>
  </v-app>
</template>

<script>
import AppBar from "./components/AppBar";
export default {
  components: {
    AppBar
  },
  data: () => ({}),
  mounted() {}
};
</script>

<style>
html {
  overflow: hidden;
}
::-webkit-scrollbar {
  width: 4px;
  background: transparent;
}
::-webkit-scrollbar-thumb {
  background: #05386b;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
