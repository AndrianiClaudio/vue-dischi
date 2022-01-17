<template>
  <div class="card">
      <img :src="card.poster" alt="IMG">
      <h2>{{card.title}}</h2>
      <span>{{card.author}}</span>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    card: Object,
  },
};
</script>

<style></style>
