<template>
  <div class="card">
    {{ info.title }}
    {{ info.origina_title }}
    {{ info.original_language }}
    {{ info.language }}
    {{ info.vote_average }}
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    info: Object,
  },
};
</script>

<style>

</style>
