<template>
  <div class="card">
    <h2>
      {{ info.title }}
    </h2>
    <h3>
      {{ info.original_title }}
    </h3>
    <div class="language">
      <!-- <img src="../assets/images/en.png" alt=""> -->
      <img
        v-if="isAvailable"
        :src="require(`../assets/images/${info.original_language}.png`)"
        :alt="info.original_title"
      >
      <p v-else>
        {{ info.original_language }}
      </p>
    </div>
    <div class="vote">
      {{ info.vote_average }}
    </div>
  </div>
</template>

<script>
/**
 * TODO
 * Trasformiamo la stringa statica della lingua in una vera
 * e propria bandiera della nazione corrispondente,
 * gestendo il caso in cui non abbiamo la bandiera della nazione
 * ritornata dall’API (le flag non ci sono in FontAwesome).
 * "original_language": "de"
 */
export default {
  name: 'Card',
  props: {
    info: Object,
  },
  data() {
    return {
      availableLanguage: [
        'en',
        'it',
      ],
    };
  },
  computed: {
    isAvailable() {
      if (this.availableLanguage.includes(this.info.original_language)) {
        return true;
      }
      return false;
    },
  },
};
</script>

<style>

</style>
