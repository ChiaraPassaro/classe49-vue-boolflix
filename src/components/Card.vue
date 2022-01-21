<template>
  <div class="card">
    <h2>
      Title: {{ (info.title) ? info.title : info.name }}
      <!-- Title: {{ info.title }} -->
    </h2>
    <h3>
      Original title: {{ (info.original_title) ? info.original_title : info.original_name }}
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
      <font-awesome-icon
        icon="air-freshener"
      />
      {{ info.vote_average }}
    </div>
  </div>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core';
import { faAirFreshener } from '@fortawesome/free-solid-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';

library.add(faAirFreshener);
// tv
//  "name": "Goof Troop",
//  "original_name": "Goof Troop",
// movies
//  "title": "Goof Troop",
//  "original_title": "Goof Troop",
export default {
  name: 'Card',
  components: {
    FontAwesomeIcon,
  },
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

<style lang="scss">

</style>
