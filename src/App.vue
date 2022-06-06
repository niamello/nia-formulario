<template>
  <div id="app">
    <h1></h1>
    <Texts :dados="''"/>
  </div>
</template>


<script>
import Texts from './component/Texts.vue';

export default {
  name: 'App',
  components: {
    Texts
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@200;300;400;500;600&family=Open+Sans&display=swap');

*{
  padding: 0;
  margin: 0;
  font-size: 100%;
  box-sizing: border-box;
  font-family: 'inter', sans-serif;
}

body {
  width: 100%;
  height: 100vh;
}

</style>