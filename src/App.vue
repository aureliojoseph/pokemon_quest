<template>
  <h1>Pokemon Quest</h1>
  <el-input
    v-model="searchPokemons"
    placeholder="Digite o nome do Pokemon"
    class="input-with-select"
  />

  <div>
    <div
      v-for="pokemon in filteredPokemons"
      :key="pokemon.name"
    >
      <div>
        <img
          :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${getId(pokemon)}.png`"
          :alt="pokemon.name"
        >
        <p>{{getName(pokemon)}}</p>
      </div>
    </div>
  </div>

  <el-button @click="dialogVisible = true">Teste</el-button>
  <el-dialog v-model="dialogVisible">
    <h2>Teste</h2>
  </el-dialog>
</template>

<script>
  import axios from 'axios'

  export default {
    name: 'App',
    data() {
      return {
        pokemons: [],
        searchPokemons: '',
        dialogVisible: false
      }
    },
    methods: {
      getId(pokemon) {
        return Number(pokemon.url.split("/")[6])
      },
      getName(pokemon) {
        return pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1)
      },
      showDialog() {
        return !this.dialogVisible
      }
    },
    computed: {
      filteredPokemons() {
        return this.pokemons.filter((item) => {
          return item.name.includes(this.searchPokemons)
        })
      }
    },
    mounted() {
      axios
        .get("https://pokeapi.co/api/v2/pokemon?limit=500")
        .then((response) => {
          return this.pokemons = response.data.results
        })
    }
  }
</script>

<style scoped lang="scss">

</style>
