<template>
  <TradingChart></TradingChart>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import TradingChart from './components/TradingChart.vue';

export default defineComponent({
  name: 'App',
  components: { TradingChart },
});
</script>

<style>
body {
  margin: unset;
}

#app {
  width: 100vw;
  height: 100vh;
  background-color: black;
}
</style>
