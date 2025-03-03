<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <!-- <ElementUI></ElementUI> -->
    简单的表格 
    <SimpleTable></SimpleTable>
    支持编辑的表格
    <EditableTable></EditableTable>
    带分页的表格
    <PaginationTable></PaginationTable>
    双击便可进行编辑的表格
    <EditableTableWithDoubleClick></EditableTableWithDoubleClick>
  </div>
</template>

<script>
// import ElementUI from './components/ElementUI.vue';
import PaginationTable from './components/PaginationTable.vue';
import EditableTable from './components/EditableTable.vue';
import SimpleTable from './components/SimpleTable.vue';
import EditableTableWithDoubleClick from './components/EditableTableWithDoubleClick.vue';
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld,
    // ElementUI,
    SimpleTable,
    EditableTable,
    PaginationTable,
    EditableTableWithDoubleClick
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
