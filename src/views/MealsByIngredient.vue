<template>
  <div class="p-8 pb-0">
    <h1 class="text-4xl font-bold mb-4 text-orange-500">Meals for {{ ingredient.strIngredient }}</h1>
  </div>
  <Meals :meals="meals"/>
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import axiosClient from "../axiosClient";
import store from "../store";
import MealItem from "../components/MealItem.vue";
import Meals from "../components/Meals.vue";

// const ingredients = ref([]);
const meals = computed(() => store.state.mealsByIngredient);

const ingredient = computed(() => store.state.ingredient);

const route = useRoute();


// onMounted(() => {
//   axiosClient.get('list.php?i=list')
//    .then(({ data }) => {
//     ingredients.value = data.meals;

//   })
// })


onMounted(() => {

  store.dispatch('searchMealsByIngredient', route.params.ingredient);

});
</script>