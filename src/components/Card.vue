<template>
  <div class="card">
      <img src="#" alt="IMG">
      <h2>Title</h2>
      <span>Testo</span>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Card',
  created() {
    axios.get('https://flynn.boolean.careers/exercises/api/array/music')
      .then((response) => {
        console.log(response.data.response);
      });
  },
  components: {
  },
};
</script>

<style></style>
