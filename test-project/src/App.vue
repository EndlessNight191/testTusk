<template>
  <div>
    <main-page/>
  </div>
</template>

<script>
import '@/assets/main.css'
import mainPage from '@/pages/mainPage'

export default {
  name: 'App',
  components: {
    mainPage
  }
}
</script>

<style>
#app {
  font-family: Poppins, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}
</style>
