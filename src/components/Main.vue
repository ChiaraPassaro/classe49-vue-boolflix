<template>
  <main>
    <div class="cards" />
  </main>
</template>

<script>
export default {
  name: 'Main',
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
