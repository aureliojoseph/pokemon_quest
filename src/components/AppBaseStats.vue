<template>
  <div class="base-stats">
    <el-card>
      <div class="base-stats__card">
        <el-tag
          v-for="stat in selectedPokemon.stats"
          :key="stat.base_stat"
          effect="dark"
          type="warning"
          round
        >
          {{stat.stat.name}}: {{stat.base_stat}}
        </el-tag>
      </div>
    </el-card>
  </div>
</template>

<script>
export default {
  props: {
    selectedPokemon: Object
  },
  methods: {
    getName(pokemon) {
      return pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1)
    }
  }
}
</script>

<style lang="scss" scoped>
  .base-stats {
    &:deep {
      .base-stats__card {
        display: flex;
        gap: 10px;
        justify-items: center;
        flex-direction: column;
        align-items: center;
      }
    }
  }
</style>