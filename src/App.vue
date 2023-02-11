<template>
  <div class="app_container">
    <nav>
      <h1>Pokemon Quest</h1>
      <el-input
        type="text"
        v-model="searchPokemons"
        placeholder="Digite o nome do Pokemon"
        clearable
      />
    </nav>

    <div class="app_container--list">
      <div
        v-for="pokemon in filteredPokemons"
        :key="pokemon.name"
      >
        <!-- component: AppPokemonCard.vue -->
        <app-pokemon-card
          :pokemon="pokemon"
          @display-card="showPokemon"
        />
      </div>
    </div>

    <!-- component: AppPokemonCardInfo.vue -->
    <!-- <app-pokemon-card-info
      :dialogVisible="showCardInfo"
      :selectedPokemon="selectedPokemon"
    /> -->

    <el-dialog
      v-model="showCardInfo"
      width="15%"
      center
      :show-close="false"
      >
      <template #header>
        <img src="@/assets/arrow-left-thin.svg" alt="left arrow icon">
        <img src="@/assets/heart-thin.svg" alt="heart icon">
      </template>
      <div v-if="selectedPokemon">
        <el-card>
          <p>{{getName(selectedPokemon)}}</p>
          <el-tag
            v-for="type in selectedPokemon.types"
            :key="type.slot"
            effect="dark"
            round
          >
            {{type.type.name}}
          </el-tag>
          <img
            :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${selectedPokemon.id}.png`"
            :alt="selectedPokemon.name"
          >
        </el-card>
      </div>
    </el-dialog>
  </div>
</template>

<script>
  import axios from 'axios'
  import AppPokemonCard from './components/AppPokemonCard.vue'
  // import AppPokemonCardInfo from './components/AppPokemonCardInfo.vue'

  export default {
    name: 'App',
    components: {
      AppPokemonCard,
      // AppPokemonCardInfo
    },
    data() {
      return {
        pokemons: [],
        searchPokemons: '',
        showCardInfo: false,
        selectedPokemon: null
      }
    },
    methods: {
      showPokemon(id) {
        axios
        .get(`https://pokeapi.co/api/v2/pokemon/${id}`)
        .then((response) => {
          this.selectedPokemon = response.data
          return this.showCardInfo = true
        })
      },

      getName(pokemon) {
        return pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1)
      },

      closeDialog() {
        return this.showCardInfo = false
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
          this.pokemons = response.data.results
        })
    }
  }
</script>

<style scoped lang="scss">
  .app_container {
    background-color: #fff;
    padding: 0 80px 40px;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: -9px;
    
    nav {
      display: flex;
      flex-direction: column;
      align-items: center;
      margin-bottom: 1rem;
      position: fixed;
      background-color: #f8f9fa;
      width: 99%;
      box-shadow: 1px 2px 4px 0 rgba(85, 85, 85, 0.161);

      h1 {
        text-align: center;
        font-size: 2rem;
      }
      
      &:deep {
        .el-input {
          width: 30rem;
          margin-bottom: 1rem;

          .el-input__wrapper {
            background-color: #f8f9fa;
            
            .el-input__inner {
              color: #868e96;
            }
          }
        }
      }
    }

    .app_container--list {
      display: grid;
      grid-template-columns: repeat(5, 1fr);
      gap: 1rem;
      margin-top: 9rem;
    }
  }
</style>
