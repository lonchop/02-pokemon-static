<script setup lang="ts">
import { ref, onMounted, watch } from 'vue';

interface Props {
  initValue: number;
}
const props = defineProps<Props>();

const count = ref(props.initValue);

const decrement = () => {
  count.value--;
};

const increment = () => {
  count.value++;
};

</script>

<template>

  <!-- Children -->
  <slot />

  <p class="text-2xl">Count: {{ count }}</p>

  <div class="flex flex-row gap-2">
    <button class="bg-blue-500 cursor-pointer text-white p-2 rounded-md w-10" @click="decrement">-1</button>
    <button class="bg-blue-500 cursor-pointer text-white p-2 rounded-md w-10" @click="increment">+1</button>
  </div>
</template>

