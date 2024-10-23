<template>
  <div class="">
    <div v-if="pokemon">
      <img :src="pokemon.sprites.front_default" :alt="pokemon.name" class="" />
      <h2 class="">{{ pokemon.name }}</h2>
      <div class="">
        <span
          v-for="(type, index) in pokemon.types"
          :key="index"
          class=""
        >
          {{ type.type.name }}
        </span>
      </div>
      <div class="my-4">
        <h3 class="font-semibold">Base Stats:</h3>
        <ul>
          <li v-for="(stat, index) in pokemon.stats" :key="index">
            {{ stat.stat.name }}: {{ stat.base_stat }}
          </li>
        </ul>
      </div>
      <button
        class=""
        @click="loadRandomPokemon"
      >
        Load another Pokémon
      </button>
    </div>
    <div v-else>
      <p>Loading...</p>
    </div>
  </div>
</template>

<script lang="ts">
  import pokemonData from '@/stores/pokemon.json';
  export default {
    data(): {
      pokemon: typeof pokemonData | null
      randomPokemonNumber: number
      lastPokemonNumber: number
    } {
      return {
        pokemon: null,
        randomPokemonNumber: 1,
        lastPokemonNumber: 1025
      };
    },
    methods: {
      async loadRandomPokemon() {
        this.pokemon = null

        try {
          this.setRandomPokemonNumber()

          const response = await fetch(`https://pokeapi.co/api/v2/pokemon/${this.randomPokemonNumber}`)

          this.pokemon = (await response.json()) as typeof pokemonData
        } catch (e) {
          console.error(e)
        }
      },
      setRandomPokemonNumber() {
        this.randomPokemonNumber = Math.floor(
            Math.random() * (this.lastPokemonNumber - 1 + 1)
        ) + 1
      }
    },
    async mounted() {
      await this.loadRandomPokemon()
    },
  };
  </script>

<style scoped>

</style>
