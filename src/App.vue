<template>
  <div id="app">
    <Table />
    <Modal />
    <button class="btn">Добавить</button>
  </div>
</template>

<script>
import Table from './components/Table.vue'
import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: {
    Table,
    Modal
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
