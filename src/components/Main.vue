<template>
  <main class="main">
      <div class="container">
        <Card />
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
};
</script>

<style lang="scss" scoped>
@import '../assets/scss/partials/_variables.scss';

.main {
    background-color: $mainBgColor;
    .container {
        width: 60%;
        margin: 0 auto;
        padding: 3.5rem 0;
    }
}
</style>
