<script setup lang="ts">
import { ref, computed } from 'vue';
import type { FavoritePokemon } from '@interfaces/favorite-pokemons';

const props = defineProps<{
  pokemon: FavoritePokemon;
}>();

const emit = defineEmits<{
  (e: 'pokemon-removed', pokemonId: number): void;
}>();

const viewPokemon = ref(true);

const imageSrc = computed(() => {
  return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/${props.pokemon.id}.png`;
});

const removePokemon = () => {
  const favoritePokemons = localStorage.getItem('favorite-pokemons') ?? '[]';

  const parsedFavoritePokemons = JSON.parse(favoritePokemons);

  const newFavoritePokemons = parsedFavoritePokemons.filter((pokemon: FavoritePokemon) => pokemon.id !== props.pokemon.id);

  localStorage.setItem('favorite-pokemons', JSON.stringify(newFavoritePokemons));

  // viewPokemon.value = false;

  emit('pokemon-removed', props.pokemon.id);

  console.log('removePokemon', props.pokemon.id);
};

</script>

<template>
  <div class="flex flex-col items-center justify-center">
    <a :href="`/pokemons/${pokemon.name}`">
      <img 
        :src="imageSrc" 
        :alt="pokemon.name"
        width="120" 
        height="120"
        :style="`view-transition-name: ${pokemon.name}-image;`"
      />
      <p class="capitalize">{{ pokemon.id }} - {{ pokemon.name }}</p>
    </a>
    <button @click="removePokemon" class="text-red-500 p-2 rounded-md cursor-pointer">
      Borrar
    </button>
  </div>
</template>