<template>
  <main class="main">
    <div class="container">
      <Card
        v-for="(card, index) in cards"
        :key="index"
        :card = card
      />
    </div>
  </main>
</template>

<script>
import axios from 'axios';
import Card from './Card.vue';

export default {
  name: 'Main',
  components: {
    Card,
  },
  data() {
    return {
      queryApi: 'https://flynn.boolean.careers/exercises/api/array/music',
      cards: Object,
    };
  },
  mounted() {
    axios.get(this.queryApi)
      .then((result) => {
        this.cards = result.data.response;
      })
      .catch((err) => {
        console.log(err);
      });
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/partials/_variables.scss";

.main {
  background-color: $mainBgColor;
  .container {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    width: 60%;
    margin: 0 auto;
    padding: 3.5rem 0;
    gap: 1.5rem;
  }
}
</style>
