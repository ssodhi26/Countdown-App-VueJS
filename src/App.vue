<template>
  <home-component />
  <counter-component
  :year = "2024"
  :month = "10"
  :date = "15"
  :hour = "10"
  :minute = "10"
  :second = "10"
  :millisecond = "10"
  />
</template>

<script>
import HomeComponent from './components/home-component.vue'
import CounterComponent from './components/counter-component.vue'

export default {
  name: 'App',
  components: {
    HomeComponent,
    CounterComponent
  }
}
</script>

<style>
#app {
  font-family: 'Times New Roman', Times, serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #040f78;
  background: -webkit-linear-gradient(right, rgb(161, 247, 230), rgb(9, 230, 199), rgb(20, 120, 106));
}
</style>
