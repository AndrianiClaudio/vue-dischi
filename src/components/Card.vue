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

<style lang="scss" scoped>
.card {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  flex-basis: calc(100% / 5 - 2rem);
  align-items: center;
  h2 {
    text-align: center;
  }
  img {
    height: 150px;
    width: 150px;
  }
}
</style>
