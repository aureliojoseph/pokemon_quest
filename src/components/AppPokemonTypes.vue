<template>
  <el-card>
    <div class="type_card">
      <h2>{{getName(selectedPokemon)}}</h2>
      
      <div class="type_card--tag">
        <el-tag
          v-for="type in selectedPokemon.types"
          :key="type.slot"
          effect="dark"
          type="success"
          round
        >
          {{type.type.name}}
        </el-tag>
      </div>
    </div>
    <img
      :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${selectedPokemon.id}.png`"
      :alt="selectedPokemon.name"
    >
  </el-card>
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