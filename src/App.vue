

<template>
  <div id="app">
    <EmployeeGrid />
  </div>
</template>

<script>
import EmployeeGrid from './components/EmployeeGrid.vue';

export default {
  name: 'App',
  components: {
    EmployeeGrid,
  },
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  padding: 20px;
}
</style>
