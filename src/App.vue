<template>
  <container>
    <header>
      <img src="./assets/bg.png" alt="background-principal" class="background">
      <h1 class="text-h1">Pokedex</h1>
    </header>

    <main>
      <input v-model="search" class="input-search" placeholder="Pesquisar">
      <div class="principal">
        <label v-for="pokemon in filtered_pokemons" :key="pokemon.name">
          <CardPokemon :pokemon="pokemon" @clicked="showPokemon" />
        </label>
      </div>
    </main>

    <section>
      <div v-if="showModal" width="800" class="modal-overlay" @click="showModal = false">
        <div v-if="pokemonSelected" class="modal" @click.stop>
          <div class="info-pokemon">
            <img
              :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokemonSelected.id}.png`"
              :alt="pokemonSelected.name">
            <div class="text-info">
              <h2>{{ get_name(pokemonSelected) }}</h2>
              <div class="div-types">
                <label class="label-types" v-for="type in pokemonSelected.types" :key="type.slot">
                  {{ type.type.name }}
                </label>
              </div>
              <div class="div-size-pokemon">
                <label class="label">Altura {{ pokemonSelected.height * 2.54 }} cm</label>
                <label class="label">Peso {{ (pokemonSelected.weight * 0.45359237).toFixed(0) }} Kg</label>
              </div>
            </div>
          </div>

          <h2 class="stats-h2">Stats</h2>
          <Stats :pokemon="pokemonSelected" />
          <button @click="showModal = false" class="btn-closed">Fechar</button>
        </div>
      </div>
    </section>
  </container>
</template>

<script>
import axios from 'axios'
import CardPokemon from './components/CardPokemon.vue'
import Stats from './components/Stats.vue'

export default {
  name: "App",

  components: {
    CardPokemon,
    Stats,
  },

  data: () => {
    return {
      pokemons: [],
      search: "",
      showModal: false,
      pokemonSelected: null,
    }
  },

  mounted() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151').then((response) => {
      this.pokemons = response.data.results
    })
  },

  methods: {
    get_id(pokemon) {
      return Number(pokemon.url.split('/')[6])
    },

    get_name(pokemon) {
      return pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1)
    },

    showPokemon(id) {
      axios.get(`https://pokeapi.co/api/v2/pokemon/${id}`)
        .then((response) => {
          this.pokemonSelected = response.data
          this.showModal = !this.showModal
        })
    },
  },

  computed: {
    filtered_pokemons() {
      return this.pokemons.filter((item) => {
        return item.name.includes(this.search)
      })
    }
  }


}
</script>
