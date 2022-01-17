<template>
  <main class="main">
    <div class="container" v-if="dataLoad">
      <Card
        v-for="(card, index) in cards"
        :key="index"
        :card = card
      />
    </div>
    <div class="container" v-else>
      <Loader />
    </div>
  </main>
</template>

<script>
import axios from 'axios';
import Card from './Card.vue';
import Loader from './Loader.vue';

export default {
  name: 'Main',
  components: {
    Card,
    Loader,
  },
  data() {
    return {
      queryApi: 'https://flynn.boolean.careers/exercises/api/array/music',
      cards: Object,
      dataLoad: false,
    };
  },
  mounted() {
    axios.get(this.queryApi)
      .then((result) => {
        this.cards = result.data.response;
      })
      .catch((err) => {
        console.log(err);
      }).then(() => {
        this.dataLoad = true;
      });
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/partials/_variables.scss";

.main {
  min-height: calc(100vh - 80px);
  height: 100%;
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
