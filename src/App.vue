<template>
  <div id="app">
    <slide></slide>
  </div>
</template>

<script>
import slide from './components/Slide';

export default {
  name: 'app',
  components: {
    slide
  }
};
</script>

<style lang='scss'>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  color: #2c3e50;
  background-color: #fff;
}
</style>
