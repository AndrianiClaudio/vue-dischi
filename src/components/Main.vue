<template>
  <main class="main">
    <div class="container" v-if="dataLoad">
      <div class="select-container">
        <select name="select-gender" id="select-gender">
          <option v-for="(opt,index) in selectGender"
          :key="index" @click="changeSelected(index)">{{opt}}</option>
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
      genderSelectIndex: [],
      selectGender: ['all', 'Rock', 'Pop', 'Jazz', 'Metal'],
      selectGenderInd: 0,
      selectCards: null,
      tmp: null,
    };
  },
  methods: {
    filterEl(i) {
      if (i === 0 || this.tmp) {
        this.cards = this.tmp;
      }
      if (i !== 0) {
        // console.log(this.selectGender[i]);
        this.selectCards = this.cards.filter((el) => el.genre === this.selectGender[i]);
        this.tmp = this.cards;
        this.cards = this.selectCards;
      }
    },
    changeSelected(i) {
      this.selectGenderInd = i;
      this.filterEl(this.selectGenderInd);
    },
    filterByGender() {
      console.log(this.selectGenderInd);
      this.cards = this.cards.filter((el) => el.genre === this.selectGender[this.selectGenderInd]);
      // this.changeSelected();
      // console.log(this.genderSelectInd);
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
