<script setup lang="ts">
import { onMounted } from "vue";
import { useRouter, useState } from "#app";
import type { Restaurant } from "~/types/Restaurant";

const restaurants = useState<Restaurant[]>("restaurants", () => []);

const router = useRouter();

onMounted(async () => {
  if (restaurants.value.length === 0) {
    try {
      const response = await fetch("/data.json");
      restaurants.value = await response.json();
    } catch (error) {
      console.error("Erro ao carregar os dados:", error);
    }
  }
});

const columns = [
  { key: "id", label: "ID" },
  { key: "name", label: "Nome" },
  { key: "actions", label: "Ações" },
];

const goToDetails = (name: string) => {
  router.push(`/restaurants/${name}`);
};
</script>

<template>
  <div class="container mx-auto">
    <h1 class="text-2xl font-bold my-4 text-center">Top 50 Restaurants</h1>
    <UTable :columns="columns" :rows="restaurants">
      <template #actions-data="{ row }">
        <UButton @click="goToDetails(row.name)">Ver Detalhes</UButton>
      </template>
    </UTable>
  </div>
</template>
