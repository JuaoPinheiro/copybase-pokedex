<template>
    <main>
      <div @click="showPokemon(get_id(pokemon))">
        <div class="div-person">
          <img :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${get_id(pokemon)}.png`"
            :alt="pokemon.name">
          <h2>{{ get_name(pokemon) }}</h2>
        </div>
      </div>
    </main>
  </template>
  
  <script>
  
  export default {
    props: {
      pokemon: Object,
      flat: {
        type: Boolean,
        default: false,
      },
    },
    methods: {
      get_id(pokemon) {
        return Number(pokemon.url.split("/")[6]);
      },
      get_name(pokemon) {
        return pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1);
      },
      showPokemon(id) {
        this.$emit("clicked", id);
      },
    },
  };
  </script>