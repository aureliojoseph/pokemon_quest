<template>
  <div class="poke_card">
    <el-card @click="showPokemon(getId(pokemon))">
      <img
        :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${getId(pokemon)}.png`"
        :alt="pokemon.name"
      >
      <h2>{{getName(pokemon)}}</h2>
    </el-card>
  </div>
</template>

<script>
  export default {
    name: 'AppPokemonCard',
    props: {
      pokemon: Object
    },
    emits: [
      'displayCard'
    ],
    methods: {
      getId(pokemon) {
        return Number(pokemon.url.split("/")[6])
      },

      getName(pokemon) {
        return pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1)
      },

      showPokemon(id) {
        this.$emit('displayCard', id)
      }
    }
  }
</script>

<style lang="scss" scoped>
  .poke_card {
    &:deep {
      .el-card {
        background-color: #f3f0ff;
        cursor: pointer;
        transition: all 0.2s;

        .el-card__body {
          display: flex;
          flex-direction: column;
          align-items: center;
        }
      }

      .el-card:hover {
        transform: translateY(-3%);
      }
    }
  }
</style>