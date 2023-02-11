<template>
  <div>
    <el-dialog
      v-model="dialogVisible"
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
          <h1>{{getName(selectedPokemon)}}</h1>

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

          <!-- component: AppAbout.vue -->

          <!-- component: AppBaseStats.vue -->
        </el-card>
      </div>
    </el-dialog>
  </div>
</template>

<script>
  export default {
    name: 'AppPokemonCardInfo',
    emits: [
      'dialogVisible'
    ],
    props: {
      dialogVisible: Boolean,
      selectedPokemon: Object
    },
    methods: {
      getName(pokemon) {
        return pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1)
      }
    },
    watch: {
      dialogVisible() {
        this.$emit("update:dialogVisible", this.dialogVisible);
      },
    }
  }
</script>

<style lang="scss" scoped>

</style>