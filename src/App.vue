<template>
  <div id="app">
    <!-- versione con invio delle card e chiamata alla API in App -->
    <Header @searchPerformed="search($event)" />
    <Main
      :movies="movies"
      :tvs="tvs"
    />
    <!-- Versione con watch inviamo il testo di ricerca e facciamo chiamata API in Main -->
    <!-- <Header @searchPerformed="setTextSearch($event)" /> -->
    <!-- <MainWatch :search-text="searchText" /> -->
    <Footer />
  </div>
</template>

<script>
/**
 * TODO
 * Milestone 2:
 *
 * Allarghiamo poi la ricerca anche alle serie tv. Con la stessa azione di ricerca
 * dovremo prendere sia i film che corrispondono alla query, sia le serie tv,
 * stando attenti ad avere alla fine dei valori simili
 * (le serie e i film hanno campi nel JSON di risposta diversi, simili ma non sempre identici)
 *
 *
*/

import axios from 'axios';
import Header from './components/Header.vue';
import Main from './components/Main.vue';
import Footer from './components/Footer.vue';
// import MainWatch from './components/MainWatch.vue';

export default {
  name: 'App',
  components: {
    Header,
    Main,
    Footer,
  },
  // components: { // se vogliamo usare MainWatch dobbiamo cambiare anche i components
  //   Header,
  //   MainWatch,
  //   Footer,
  // },
  data() {
    return {
      query: 'https://api.themoviedb.org/3/search/',
      api_key: 'e99307154c6dfb0b4750f6603256716d',
      language: 'en-US',
      searchText: '',
      cards: [],
      movies: [],
      tvs: [],
    };
  },
  computed: {
    getResults() {
      console.log([...this.movies, ...this.tvs]);
      return [...this.movies, ...this.tvs];
    },
  },
  created() {
    // this.getFilms(); //testiamo il nostro metodo
  },
  methods: {
    /**
     * Usando il componente MainWatch abbiamo bisogno
     * di assegnare il nuovo valore di ricerca all'emit dell'evento searchPerformed
    */
    setTextSearch(value) {
      this.searchText = value;
    },
    /**
     * questo metodo ci consente di aggiungere più ricerche
     * nel momento in cui si avvia l'evento searchPerformed
     */
    search(text) {
      this.searchText = text;
      this.getFilms();
      this.getTvs();
    },
    getFilms() {
      console.log('films');
      const endpoint = 'movie';
      // facciamo sempre attenzione a che parametri accetta la nostra API
      const parameters = {
        api_key: this.api_key,
        language: this.language,
        query: this.searchText,
      };

      /**
       * questo è l'endpoint completo
       * https://api.themoviedb.org/3/search/movie
       * al quale poi aggiungere i parametri
       * Una chiamata axios accetta una serie di parametri che possiamo trovare in documentazione
       * https://axios-http.com/docs/example
      */
      axios.get(`${this.query}${endpoint}`,
        { params: parameters })
        .then((result) => {
          this.movies = result.data.results;
          // this.cards = [...this.movies, ...this.tvs];
          console.log(this.movies);
        })
        .catch((error) => console.log(error));
    },
    getTvs() {
      console.log('tvs');

      const endpoint = 'tv';
      // facciamo sempre attenzione a che parametri accetta la nostra API
      const parameters = {
        api_key: this.api_key,
        language: this.language,
        query: this.searchText,
      };

      /**
       * questo è l'endpoint completo
       * https://api.themoviedb.org/3/search/tv
       * al quale poi aggiungere i parametri
       * Una chiamata axios accetta una serie di parametri che possiamo trovare in documentazione
       * https://axios-http.com/docs/example
      */
      axios.get(`${this.query}${endpoint}`,
        { params: parameters })
        .then((result) => {
          this.tvs = result.data.results;
          console.log(this.tvs);
          // this.cards = [...this.movies, ...this.tvs];
        })
        .catch((error) => console.log(error));
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
