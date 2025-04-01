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
    双击便可进行编辑的表格1
    <!-- <EditableTableWithDoubleClick></EditableTableWithDoubleClick> -->
    双击便可进行编辑的表格2
    <EditableTableWithDoubleClick2></EditableTableWithDoubleClick2>
    双击便可进行编辑且有分页的表格
    <EditableTableWithDoubleClickAndPagination></EditableTableWithDoubleClickAndPagination>
    
    <TableA></TableA>
  </div>
</template>

<script>
// import ElementUI from './components/ElementUI.vue';
import PaginationTable from './components/PaginationTable.vue';
import EditableTable from './components/EditableTable.vue';
import SimpleTable from './components/SimpleTable.vue';
// import EditableTableWithDoubleClick from './components/EditableTableWithDoubleClick.vue';
import EditableTableWithDoubleClick2 from './components/EditableTableWithDoubleClick2.vue';
import EditableTableWithDoubleClickAndPagination from './components/EditableTableWithDoubleClickAndPagination.vue';
import TableA from './components/TableA.vue';
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld,
    // ElementUI,
    SimpleTable,
    EditableTable,
    PaginationTable,
    // EditableTableWithDoubleClick,
    EditableTableWithDoubleClick2,
    EditableTableWithDoubleClickAndPagination,
    TableA,
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
