<template>
  <div id="app">
    <ApiSearch />
    <FooterCont />
  </div>
</template>

<script>
import ApiSearch from './components/ApiSearch'
import FooterCont from './components/FooterCont'

export default {
  name: 'app',
  components: {
    ApiSearch,
    FooterCont
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
