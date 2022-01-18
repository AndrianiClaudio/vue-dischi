<template>
  <main class="main">
    <div class="container" v-if="dataLoad">
      <div class="select-container">
        <label for="select-gender">
          Genere
        </label>
        <select name="select-gender" id="select-gender">
          <option v-for="(opt,index) in selectGender"
          :key="index" @click="changeSelectedGen(index)">{{opt}}</option>
        </select>
        <label for="select-artist">
          Artisti
        </label>
        <select name="select-artist" id="select-artist">
          <option v-for="(opt,index) in selectArtist"
          :key="index" @click="changeSelectedArt(index)">{{opt}}</option>
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
      // selectGender: ['all', 'Rock', 'Pop', 'Jazz', 'Metal'],
      selectGender: ['all'],
      selectArtist: ['all'],
      selectGenderInd: 0,
      selectArtistInd: 0,
      selectCards: null,
      tmp: null,
    };
  },
  methods: {
    filterEl(i, type) {
      if (i === 0 || this.tmp) {
        this.cards = this.tmp;
      }
      if (type === 'gender') {
        if (i !== 0) {
          this.selectCards = this.cards.filter((el) => el.genre === this.selectGender[i]);
          this.tmp = this.cards;
          this.cards = this.selectCards;
        }
      } else if (type === 'artist') {
        this.selectCards = this.cards.filter((el) => el.author === this.selectArtist[i]);
        this.tmp = this.cards;
        this.cards = this.selectCards;
      }
    },
    changeSelectedGen(i) {
      this.selectGenderInd = i;
      this.filterEl(this.selectGenderInd, 'gender');
    },
    changeSelectedArt(i) {
      this.selectArtistInd = i;
      this.filterEl(this.selectArtistInd, 'artist');
    },
    filterByGender() {
      this.cards = this.cards.filter((el) => el.genre === this.selectGender[this.selectGenderInd]);
    },
    setSelectGender() {
      this.cards.forEach((element) => {
        if (!this.selectGender.includes(element.genre)) {
          this.selectGender.push(element.genre);
        }
      });
    },
    setSelectArtist() {
      this.cards.forEach((element) => {
        if (!this.selectArtist.includes(element.author)) {
          this.selectArtist.push(element.author);
        }
      });
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
        this.setSelectGender();
        this.setSelectArtist();
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
      label {
        color: white;
        text-transform: uppercase;
        display: block;
      }
      #select-gender,
      #select-artist {
        width: 10rem;
        padding: .5rem;
        text-align: center;
        font-size: 1.15rem;
      }
    }
  }
}
</style>
