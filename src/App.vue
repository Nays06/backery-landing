<template>
  <Header />
  <Main />
  <Footer />
</template>

<script>
import Footer from './components/Footer.vue';
import Header from './components/Header.vue';
import Main from './components/Main.vue';

export default {
  components: {
    Header,
    Main,
    Footer
  }
}
</script>

<style scoped>
</style>
