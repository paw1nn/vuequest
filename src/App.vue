<template>
  <div id="app">
    <DrawingBoard />
  </div>
</template>

<script>
import DrawingBoard from './components/DrawingBoard.vue';

export default {
  components: {
    DrawingBoard,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
