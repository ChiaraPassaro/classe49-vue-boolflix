<template>
  <div id="app">
    <Header />
    <Main />
    <Footer />
  </div>
</template>

<script>
import axios from 'axios';
import Header from './components/Header.vue';
import Main from './components/Main.vue';
import Footer from './components/Footer.vue';

export default {
  name: 'App',
  components: {
    Header,
    Main,
    Footer,
  },
  data() {
    return {
      query: 'https://api.themoviedb.org/3/search/',
      api_key: 'e99307154c6dfb0b4750f6603256716d',
    };
  },
  created() {
    this.getFilms();
  },
  methods: {
    getFilms() {
      const endpoint = 'movie';
      const parameters = {
        api_key: this.api_key,
        language: 'en-US',
        query: 'testo',
      };
      axios.get(`${this.query}${endpoint}`, { params: parameters }).then((result) => console.log(result)).catch((error) => console.log(error));
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
