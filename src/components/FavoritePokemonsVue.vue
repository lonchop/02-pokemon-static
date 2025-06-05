<script setup lang="ts">
import { ref, onMounted } from 'vue'
import type { FavoritePokemon } from '@interfaces/favorite-pokemons'
import FavoritePokemonVue from './FavoritePokemonVue.vue'
const favoritePokemons = ref<FavoritePokemon[]>([])

const getLocalStoragePokemons = () => {
  const pokemons = localStorage.getItem('favorite-pokemons') ?? '[]'

  return JSON.parse(pokemons)
}

onMounted(() => {
  favoritePokemons.value = getLocalStoragePokemons()
})

const onPokemonRemoved = (pokemonId: number) => {
  favoritePokemons.value = favoritePokemons.value.filter(
    (pokemon) => pokemon.id !== pokemonId,
  )

  // if (!document.startViewTransition) {
  //   favoritePokemons.value = favoritePokemons.value.filter(
  //     (pokemon) => pokemon.id !== pokemonId,
  //   )
  //   return;
  // }

  // document.startViewTransition(() => {
  //   favoritePokemons.value = favoritePokemons.value.filter(
  //     (pokemon) => pokemon.id !== pokemonId,
  //   )
  // })

}
</script>

<template>
  <div
    class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-4"
  >
    <div
      v-for="pokemon in favoritePokemons"
      :key="pokemon.id"
    >
      <FavoritePokemonVue
        :pokemon="pokemon"
        @pokemon-removed="onPokemonRemoved"
      />
    </div>
  </div>
</template>
