<template>
  <div id="app">
    <comp-header firstText="入力欄" secondText="Input Field"/>
  </div>
</template>

<script>
import CompHeader from './components/CompHeader.vue';
export default {
  name: "App",
  components: {
    CompHeader
  },
};
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center; 
}
</style>
