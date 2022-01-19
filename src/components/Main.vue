<template>
  <main class="main">
    <div class="container" v-if="dataLoad">
      <div class="select-container">
        <Select
        :cards = cards
        type = gender
        @filter-gender= 'changeIndex($event,"gender")'
        />
        <Select
        :cards = cards
        type = artist
        @filter-artist= 'changeIndex($event,"artist")'
        />
      </div>
      <Card
        v-for="(card, index) in filter_var"
        :key="'card'+index"
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
import Select from './Select.vue';

export default {
  name: 'Main',
  components: {
    Card,
    Loader,
    Select,
  },
  data() {
    return {
      queryApi: 'https://flynn.boolean.careers/exercises/api/array/music',
      cards: Object,
      dataLoad: false,
      filter_var: Object,
    };
  },
  methods: {
    filter(checkEl, type) {
      // console.log(checkEl, type, 'filter');
      switch (type) {
        case 'gender':
          this.filter_var = this.cards.filter((el) => el.genre === checkEl);
          break;
        case 'artist':
          this.filter_var = this.cards.filter((el) => el.artist === checkEl);
          break;
        default:
          console.log('errore... switch select type in default case');
          break;
      }
      this.filter_var = this.cards.filter((el) => {
        if (type === 'artist') {
          return el.author === checkEl;
        } if (type === 'gender') {
          return el.genre === checkEl;
        }
        return console.error('errore!!!fun_filter in Main.vue');
      });
    },
    changeIndex(e, type) {
      if (e === 'all') { this.filter_var = this.cards; } else { this.filter(e, type); }
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
        this.filter_var = this.cards;
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
      label {
        color: white;
        text-transform: uppercase;
        display: block;
      }
 }
  }
}
</style>
