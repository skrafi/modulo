<template>
  <div id="app">
    <HelloWorld msg="Modulo app" />
    <ModuloTable />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import ModuloTable from "./components/ModuloTable.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    ModuloTable
  }
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
