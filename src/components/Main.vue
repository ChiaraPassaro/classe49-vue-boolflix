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
import Card from './Card.vue';

export default {
  name: 'Main',
  components: {
    Card,
  },
  props: {
    cards: {
      type: Array,
      default() {
        return [];
      },
    },
  },
};
</script>

<style>

</style>
