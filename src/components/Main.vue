<template>
  <main class="main">
    <div class="container" v-if="dataLoad">
      <div class="select-container">
        <select name="select-gender" id="select-gender"
        @change="filterByGender">
          <option value="all">All</option>
          <option value="rock">Rock</option>
          <option value="pop">Pop</option>
          <option value="jazz">Jazz</option>
          <option value="metal">Metal</option>
        </select>
      </div>
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
  methods: {
    filterByGender() {
      console.log('in filter');
    },
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
  display: flex;
  align-items: center;
  min-height: calc(100vh - 80px);
  justify-content:center;
  height: 100%;
  // flex-direction: column;
  padding-top: 3rem;
  background-color: $mainBgColor;
  .container {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    width: 60%;
    margin: 0 auto;
    padding: 3.5rem 0;
    gap: 1.5rem;
    .select-container {
      width: 100%;
      text-align: center;
      #select-gender {
        width: 10rem;
        padding: .5rem;
        text-align: center;
        font-size: 1.15rem;
      }
    }
  }
}
</style>
