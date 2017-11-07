<template>
  <div id="app">
    <ApiSearch />
    <Footer />
  </div>
</template>

<script>
import ApiSearch from './components/ApiSearch'
import Footer from './components/Footer'

export default {
  name: 'app',
  components: {
    ApiSearch,
    Footer
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
