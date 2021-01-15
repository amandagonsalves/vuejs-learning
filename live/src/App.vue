<template>
  <div>
    <h1>My list</h1>
    <input 
      @keyup.enter="addFood" 
      type="text" 
      v-model="currentFood" />
    <button @click="addFood">Add</button>

    <FoodsList 
      @stop="handleStop"
      :foods="foods" />
  </div>
</template>

<script>
import FoodsList from './components/FoodsList.vue';

export default {
  components: {
    FoodsList,
  },

  data: () => ({
    foods: ["Maçã", "Banana", "Abacaxi", "Pera", "Morango"],
    currentFood: "",
  }),

  methods: {
    addFood() {
      this.foods.push(this.currentFood);
      this.currentFood = "";
    },

    handleStop(payload) {
      console.log('payload =>', payload);
      window.alert(payload)
    }
  },
};
</script>
