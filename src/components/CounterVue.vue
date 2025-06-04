<script setup lang="ts">
import { ref } from 'vue';

const count = ref(0);

const decrement = () => {
  count.value--;
};

const increment = () => {
  count.value++;
};

</script>

<template>
  <h1 class="text-4xl font-bold">Counter</h1>
  <p class="text-2xl">Count: {{ count }}</p>

  <div class="flex flex-row gap-2">
    <button class="bg-blue-500 cursor-pointer text-white p-2 rounded-md w-10" @click="decrement">-1</button>
    <button class="bg-blue-500 cursor-pointer text-white p-2 rounded-md w-10" @click="increment">+1</button>
  </div>
</template>

