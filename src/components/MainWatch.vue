<template>
  <main>
    <div
      v-if="cards.length > 0"
      class="cards/"
    >
      <Card
        v-for="(card, index) in cards"
        :key="index"
        :info="card"
      />
    </div>
    <div v-else>
      Nessun risultato
    </div>
  </main>
</template>

<script>
import axios from 'axios';
import Card from './Card.vue';

export default {
  name: 'MainWatch',
  components: {
    Card,
  },
  props: {
    searchText: {
      type: String,
    },
  },
  data() {
    return {
      query: 'https://api.themoviedb.org/3/search/',
      api_key: 'e99307154c6dfb0b4750f6603256716d',
      language: 'en-US',
      cards: [],
    };
  },
  /** Il Watch funziona come una computed, ma può richiamare
   ** delle funzioni con side effects e assegnare valori.
   ** Qui rimaniamo in ascolto della prop searchText,
   ** quando cambia allora si avvia il metodo search
   ** da notare come a differenza delle computed, che hanno bisogno di un
   ** nome diverso dalla proprieta' della quale rimangono in ascolto,
   ** qui abbiamo lo stesso nome della props
  */
  watch: {
    searchText() {
      this.search();
    },
  },
  methods: {
    search() {
      this.getFilms();
    },
    getFilms() {
      const endpoint = 'movie';
      const parameters = {
        api_key: this.api_key,
        language: this.language,
        query: this.searchText,
      };
      // https://api.themoviedb.org/3/search/movie
      axios.get(`${this.query}${endpoint}`, { params: parameters }).then((result) => {
        this.cards = result.data.results;
      }).catch((error) => console.log(error));
    },
  },
};
</script>

<style>

</style>
