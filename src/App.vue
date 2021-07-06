<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" id="vueLogo" >
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <stickynote />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import stickynote from './components/ToDoApp.vue'

export default {
  name: 'noteApp',
  components: {
    stickynote
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  /* -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale; */
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#vueLogo {
  height: 70px;
}

</style>
