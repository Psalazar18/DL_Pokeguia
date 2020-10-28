<template>
  <div id="app">
    <img class="mt-5" alt="Vue logo" src="https://external-preview.redd.it/tQged7mKJ3cUpNMq5IMeceZvyKP3cTyHqhNmKEQ0Vv8.png?auto=webp&s=fb5fd61cae0bc9cde2bc2a006b1e2aeb0c935ce9">
    <Pokeguia/>
  </div>
</template>

<script>
import Pokeguia from './components/Pokeguia.vue'

export default {
  name: 'App',
  components: {
    Pokeguia
  }
}
</script>

<style scoped>
img{
  width: 40%;
  margin-left: 30%;
}
</style>
