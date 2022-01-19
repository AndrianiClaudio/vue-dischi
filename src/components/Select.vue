<template>
  <label :for="`select-${type}`">
    {{type}}
    <select :name="`select-${type}`" :id="`select-${type}`">
        <option v-for="(opt,index) in options"
        :key="`${type}-${index}`"
        @click="$emit(`filter-${type}`,$event.target.value)"
        >{{opt}}</option>
    </select>
  </label>
</template>

<script>
export default {
  name: 'Select',
  props: {
    cards: Array,
    type: String,
  },
  data() {
    return {
      options: ['all'],
      selected: 'all',
    };
  },
  methods: {
    setOptions() {
      if (this.type === 'gender') {
        this.cards.forEach((el) => {
          if (!this.options.includes(el.genre)) {
            this.options.push(el.genre);
          }
        });
      } else if (this.type === 'artist') {
        this.cards.forEach((el) => {
          if (!this.options.includes(el.author)) {
            this.options.push(el.author);
          }
        });
      }
    },
  },
  mounted() {
    this.setOptions();
  },
};
</script>

<style lang="scss" scoped>
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
        text-transform: capitalize;
      }
    }
</style>
