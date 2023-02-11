<template>
  <h1>Pokemon Quest asdasd</h1>
  <el-input
    v-model="input3"
    placeholder="Please input"
    class="input-with-select"
  />

  <el-button @click="dialogVisible = true">Teste</el-button>
  <el-dialog v-model="dialogVisible">
    <h2>Teste</h2>
  </el-dialog>
</template>

<script>
  export default {
    data() {
      return {
        dialogVisible: false
      }
    },
    methods: {
      showDialog() {
        return !this.dialogVisible
      }
    }
  }
</script>

<style scoped lang="scss">

</style>
