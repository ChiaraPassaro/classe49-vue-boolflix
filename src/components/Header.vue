<template>
  <header>
    <div class="search">
      <input
        v-model="textSearch"
        type="text"
        placeholder="Inserisci un testo"
      >
      <button
        @click="$emit('searchPerformed', textSearch)"
      >
        Cerca
      </button>
    </div>
  </header>
</template>

<script>
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
