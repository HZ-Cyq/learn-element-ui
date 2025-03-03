<template>
    <div>
      <el-table :data="tableData" border style="width: 100%">
        <el-table-column prop="date" label="日期" width="180">
          <template v-slot="scope">
            <span v-if="!scope.row.editingDate" @dblclick="enableEdit(scope.row, 'date')">
              {{ scope.row.date }}
            </span>
            <el-input
              v-else
              v-model="scope.row.date"
              size="mini"
              @blur="disableEdit(scope.row, 'date')"
              @keydown.enter.native="disableEdit(scope.row, 'date')"
              ref="dateInput"
            />
          </template>
        </el-table-column>
  
        <el-table-column prop="name" label="姓名" width="180">
          <template v-slot="scope">
            <span v-if="!scope.row.editingName" @dblclick="enableEdit(scope.row, 'name')">
              {{ scope.row.name }}
            </span>
            <el-input
              v-else
              v-model="scope.row.name"
              size="mini"
              @blur="disableEdit(scope.row, 'name')"
              @keydown.enter.native="disableEdit(scope.row, 'name')"
              ref="nameInput"
            />
          </template>
        </el-table-column>
  
        <el-table-column prop="address" label="地址">
          <template v-slot="scope">
            <span v-if="!scope.row.editingAddress" @dblclick="enableEdit(scope.row, 'address')">
              {{ scope.row.address }}
            </span>
            <el-input
              v-else
              v-model="scope.row.address"
              size="mini"
              @blur="disableEdit(scope.row, 'address')"
              @keydown.enter.native="disableEdit(scope.row, 'address')"
              ref="addressInput"
            />
          </template>
        </el-table-column>
      </el-table>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        tableData: [
          { date: "2024-03-01", name: "张三", address: "北京市朝阳区", editingDate: false, editingName: false, editingAddress: false },
          { date: "2024-03-02", name: "李四", address: "上海市浦东新区", editingDate: false, editingName: false, editingAddress: false },
          { date: "2024-03-03", name: "王五", address: "广州市天河区", editingDate: false, editingName: false, editingAddress: false }
        ]
      };
    },
    methods: {
      enableEdit(row, field) {
        // this.$set(row, `editing${field.charAt(0).toUpperCase() + field.slice(1)}`, true);
        row[`editing${field.charAt(0).toUpperCase() + field.slice(1)}`] = true;
        this.$nextTick(() => {
          this.$refs[`${field}Input`] && this.$refs[`${field}Input`].focus();
        });
      },
      disableEdit(row, field) {
        this.$set(row, `editing${field.charAt(0).toUpperCase() + field.slice(1)}`, false);
      }
    }
  };
  </script>
  