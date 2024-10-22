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
      >
        Load another Pokémon
      </button>
    </div>
    <div v-else>
      <p>Loading...</p>
    </div>
  </div>
</template>

<script>
  import pokemonData from '@/stores/pokemon.json';
  export default {
    data() {
      return {
        pokemon: pokemonData,
      };
    },
    methods: {      
      
    },
    mounted() {
      
    },
  };
  </script>

<style scoped>

</style>
