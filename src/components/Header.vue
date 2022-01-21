<template>
  <header>
    <div class="search">
      <input
        v-model="textSearch"
        type="text"
        placeholder="Inserisci un testo"
      >
      <!-- Al click inviamo un emit che intercetteremo nel genitore,
      passiamo anche il dato textSearch che è collegato con l'input
      attraverso il v-model -->
      <button
        @click="$emit('searchPerformed', textSearch)"
      >
        Cerca
      </button>
    </div>
  </header>
</template>

<script>
/**
 * Questo componente non riceve props dal genitore ma ha solo un data interno
 */
export default {
  name: 'Header',
  data() {
    return {
      textSearch: '',
    };
  },
};
</script>

<style>

</style>
