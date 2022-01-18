<template>
  <div class="card">
      <img :src="card.poster" alt="IMG">
      <h2>{{card.title}}</h2>
      <div class="sub-info">
        <span>{{card.author}}</span>
        <span>{{card.year}}</span>
      </div>
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
@import "../assets/scss/partials/_variables.scss";
.card {
  background-color: $cardBgColor;
  display: flex;
  flex-direction: column;
  flex-basis: calc(100% / 5 - 2rem);
  align-items: center;
  padding: 1.25rem;
  gap: 0.75rem;
  img {
    height: 150px;
    width: 150px;
  }
  h2 {
    font-size: 1.2rem;
    text-align: center;
    text-transform: uppercase;
    color: white;
  }
  .sub-info {
    span {
      display: block;
      text-align: center;
      color: grey;
      font-size:0.95rem;
    }
  }
}
</style>
