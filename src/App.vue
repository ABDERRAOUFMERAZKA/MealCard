<template>
  <div id="app">
    <CardMeal />
  </div>
</template>

<script>
import CardMeal from './components/mealCard.vue'

export default {
  name: 'app',
  components: {
    CardMeal
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
