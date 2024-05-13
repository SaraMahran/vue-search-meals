<template>
  <div class="max-w-[800px] mx-auto p-8">
    <h1 class="text-5xl font-bold mb-5 text-orange-500">{{ meal.strMeal }}</h1>
    <img :src="meal.strMealThumb" :alt="meal.strMeal" class="max-w-[100%]"/>
    <div class="grid grid-cols-1 sm:grid-cols-3 tx-lg py-2">
      <div>
        <strong class="font-bold text-orange-500">Category: </strong>
        <p class="inline">{{ meal.strCategory }}</p>
      </div>
      <div>
        <strong class="font-bold text-orange-500">Area: </strong>
        <p class="inline">{{ meal.strArea }}</p>
      </div>
      <div>
        <strong class="font-bold text-orange-500">Tags: </strong>
        <p class="inline">{{ meal.strTags }}</p>
      </div>
    </div>
    <div class="my-3">
      {{ meal.strInstructions }}
    </div>
    <div class="grid grid-cols-1 sm:grid-cols-2">
      <div>
        <h2 class="text-2xl font-semibold mb-2 text-orange-500">Ingredients</h2>
        <ul>
          <template v-for="(el, index) in new Array(20)" :key="index">
            <li v-if="meal[`strIngredient${index + 1}`]">
              {{ index + 1 }}. {{ meal[`strIngredient${index + 1}`] }}
            </li>
          </template>
          <div class="mt-6">
            <YouTubeButton :href="meal.strYoutube">YouTube</YouTubeButton>
          </div>
        </ul>
      </div>
      <div>
        <h2 class="text-2xl font-semibold mb-2 text-orange-500">Measures</h2>
        <ul>
          <template v-for="(el, index) in new Array(20)" :key="index">
            <li v-if="meal[`strMeasure${index + 1}`]">
              {{ index + 1 }}. {{ meal[`strMeasure${index + 1}`] }}
            </li>
          </template>
          <div class="mt-6">
            <a
              :href="meal.strSource"
              target="_blank"
              class="px-3 py-3 rounded border-2 border-orange-200 bg-orange-500 text-white hover:bg-orange-600 hover:text-white transition-colors"
            >
              View Original Source
            </a>
          </div>
        </ul>
      </div>
    </div>
    
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";
import axiosClient from "../axiosClient";
import YouTubeButton from "../components/YouTubeButton.vue";

const route = useRoute();
const meal = ref({});

onMounted(() => {
  axiosClient.get(`lookup.php?i=${route.params.id}`).then(({ data }) => {
    debugger;
    meal.value = data.meals[0] || {};
  });
});
</script>
