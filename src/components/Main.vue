<template>
  <main>
    <div class="movies">
      <h2>Movies</h2>
      <div
        v-if="movies.length > 0"
        class="cards/"
      >
        <Card
          v-for="(card, index) in movies"
          :key="index+'-'+card.id"
          :info="card"
        />
      </div>
      <div v-else>
        Nessun risultato
      </div>
    </div>
    <div class="series">
      <h2>TV</h2>
      <div
        v-if="tvs.length > 0"
        class="cards/"
      >
        <Card
          v-for="(card, index) in tvs"
          :key="index+'-'+card.id"
          :info="card"
        />
      </div>
      <div v-else>
        Nessun risultato
      </div>
    </div>
  </main>
</template>

<script>
import Card from './Card.vue';

export default {
  name: 'Main',
  components: {
    Card,
  },
  /**
   * Per assegnare un valore di default ad un array o un object
   * è necessario utilizzare una funzione che restituisce
   * l'array o object stesso
   */
  props: {
    movies: {
      type: Array,
      default() {
        return [];
      },
    },
    tvs: {
      type: Array,
      default() {
        return [];
      },
    },
  },
};
</script>

<style lang="scss">

</style>
