<template>
  <div id="app">
    <img alt="phonebook logo" src="./assets/logo.jpg">
    <Phonebook msg="Phonebook v1"/>
  </div>
</template>

<script>
import Phonebook from './components/Phonebook.vue'

export default {
  name: 'app',
  components: {
    Phonebook
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

#app img {
  width: 100px;
  margin-top: -50px;
  margin-bottom: -20px;
}
</style>
