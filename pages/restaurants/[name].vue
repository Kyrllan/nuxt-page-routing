<script setup lang="ts">
import { useRoute, useRouter, useState } from "#app";
import type { Restaurant } from "~/types/Restaurant";

const route = useRoute();
const restaurants = useState<Restaurant[]>("restaurants");

const restaurant = restaurants.value.find(
  (r) => r.name === String(route.params.name)
);
</script>

<template>
  <div v-if="restaurant" class="container mx-auto">
    <div class="restaurant-container">
      <div class="image-container">
        <img :src="restaurant.imageUrl" alt="Restaurante" />
      </div>
      <div class="info-container">
        <h1 class="title">{{ restaurant.name }}</h1>
        <div class="stats-container">
          <h5>Revenue (in billions)</h5>
          <p>${{ restaurant.revenue.toLocaleString() }}</p>
        </div>
        <div class="stats-container">
          <h5>Number of Stores</h5>
          <p>{{ restaurant.numberOfStores }}</p>
        </div>
        <p class="content">{{ restaurant.content }}</p>
      </div>
    </div>
  </div>
  <div v-else class="text-center text-red-500">Restaurante não encontrado</div>
</template>

<style scoped>
.restaurant-container {
  display: flex;
}
.image-container {
  width: 75%;
  height: calc(100vh - 60px);
  position: relative;
  overflow: hidden;
}
.image-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.info-container {
  padding: 3rem;
  width: 50%;
}
.title {
  line-height: 6rem;
}
.info-container h1 {
  text-transform: uppercase;
  font-size: 6rem;
  margin-bottom: 3rem;
}
.stats-container {
  display: flex;
  align-items: flex-end;
  margin-bottom: 1rem;
}
.stats-container h5 {
  width: 20rem;
  font-size: 2rem;
  margin: 0;
  margin-right: 5rem;
}
.stats-container p {
  font-size: 2rem;
  margin: 0;
}
.content {
  font-size: 1.25rem;
  margin-top: 3rem;
}
</style>
