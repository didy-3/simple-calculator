<template>
  <SimpleCalculator />
</template>

<script>
import SimpleCalculator from "@/components/SimpleCalculator";

export default {
  name: 'App',
  components: {
    SimpleCalculator
  }
}
</script>

<style lang="scss">
body{
  background-color: rgb(42, 30, 59, .6);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: grid;
  place-items: center;
  min-height: 98vh;
}
</style>
