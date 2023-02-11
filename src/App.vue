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

    <div
      @click="openInfoCard"
      class="app_container--list"
    >
      <div
        v-for="pokemon in filteredPokemons"
        :key="pokemon.name"
      >
        <app-pokemon-card
          :pokemon="pokemon"
          @display-card="showPokemon"
        />
      </div>
    </div>

    <el-dialog
      v-model="showCardInfo"
      width="30%"
      center
      :show-close="false"
      >

      <template #header>
        <img @click="closeInfoCard" src="@/assets/arrow-left-thin.svg" alt="left arrow icon">
        <img src="@/assets/heart-thin.svg" alt="heart icon">
      </template>

      <div v-if="selectedPokemon">
        <app-pokemon-types :selectedPokemon="selectedPokemon" />
      </div>

    </el-dialog>
  </div>
</template>

<script>
  import axios from 'axios'
  import AppPokemonCard from './components/AppPokemonCard.vue'
  import AppPokemonTypes from './components/AppPokemonTypes.vue'

  export default {
    name: 'App',
    components: {
      AppPokemonCard,
      AppPokemonTypes
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

      openInfoCard() {
        return this.showCardInfo = true
      },

      closeInfoCard() {
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

    :deep {
      .el-dialog {
        border-radius: 20px;

        .el-dialog__header {
          margin: 0;
          padding: 40px 20px 10px;
          display: flex;
          justify-content: space-between;
          background-color: #e3fafc;
          border-top-left-radius: 20px;
          border-top-right-radius: 20px;
          
          img {
            width: 18px;
            cursor: pointer;
          }
        }

        .el-dialog__body {
          padding: 0;
          background-color: #e3fafc;
          border-bottom-left-radius: 20px;
          border-bottom-right-radius: 20px;

          .el-card {
            border-radius: 20px;

            .el-card__body {
              display: flex;
              flex-direction: column;
              align-items: center;
              background-color: #0b7285;

              .type_card {
                text-align: center;

                h2 {
                  color: #fff;
                }

                .type_card--tag {
                  display: flex;
                  gap: 10px;
                }
              }
            }
          }
        }
      }
    }
  }
</style>
