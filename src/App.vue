<template>
  <div id="app">
    <Header />
    <MainContent />
    <Footer />
  </div>
</template>

<script>
  import MainContent from './components/MainContent';
  import Header from './components/Header';
  import Footer from './components/Footer';
  export default {
    name: 'App',
    components: { MainContent, Header, Footer },
  };
</script>

<style lang="scss">
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    background-color: #f3f3f3;
    min-height: 100vh;
    font-family: 'Open Sans';
  }
</style>
