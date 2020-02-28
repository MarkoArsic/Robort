<template>
  <div id="app" >
    <img alt="Vue logo" src="./assets/logo.png">
    <FileReader />
  </div>
</template>

<script>
import FileReader from './components/FileReader.vue'

export default {
  name: 'App',
  components: {
    FileReader
  }
}
</script>

<style>
*{
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
/* html,
body {
  height: 100%;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Roboto', sans-serif;
  background: linear-gradient(to top, #4F6072, #8699AA);
  display: flex;
  justify-content: center;
  align-items: center;
} */
#app {
  /*font-family: Avenir, Helvetica, Arial, sans-serif;*/
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 3rem;
}
</style>
