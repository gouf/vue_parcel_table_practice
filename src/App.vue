<template>
  <div>
    <Hello>Vue + Parcel</Hello>
    <Table></Table>
  </div>
</template>

<script>
import Hello from './components/Hello.vue'
import Table from './components/Table.vue'

export default {
  components: {
    Hello,
    Table
  }
}
</script>

<style scoped>
</style>
