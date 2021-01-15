<template>
  <ul>
    <li v-for="(food, index) in foodsWithDots" :key="`${food}-${index}`">
      {{ food }}
    </li>
  </ul>
</template>

<script>
const maxFoods = 10;

export default {
  props: {
    foods: { type: Array, default: () => [] },
  },
  data () {
    return {
    foodsWithDots: this.foods.map(food => `${food}.`) 
    }
  },
  watch: {
    foods() {
      if (this.foods.length === maxFoods) {
        this.$emit('stop', 'ta cheio')
        console.log("changed", this.foods.length);
      }
    },
  },
};
</script>
