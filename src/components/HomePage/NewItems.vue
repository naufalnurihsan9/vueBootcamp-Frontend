<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import NewItemsCard from "../NewItemsCard.vue";

const items = ref([]);

async function getNewItemsData() {
  try {
    const response = await axios.get(
      "https://zullkit-backend.buildwithangga.id/api/products"
    );
    items.value = response.data.data.data;
  } catch (error) {
    console.error(error);
  }
}

onMounted(() => {
  getNewItemsData();
});
</script>

<template>
  <div class="container px-4 mx-auto my-16 md:px-12">
    <h2 class="mb-4 text-xl font-medium md:mb-0 md:text-lg">New Items</h2>
    <div class="flex flex-wrap -mx-1 lg:-mx-4">
      <NewItemsCard
        v-for="item in items"
        :key="item.id"
        :id="item.id"
        :subtitle="item.subtitle"
        :name="item.name"
        :thumbnails="item.thumbnails"
      />
    </div>
  </div>
</template>
