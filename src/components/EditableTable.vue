<template>
    <div>
      <el-table :data="tableData" border style="width: 100%">
        <el-table-column prop="date" label="日期" width="180"></el-table-column>
        <el-table-column prop="name" label="姓名" width="180"></el-table-column>
        <el-table-column prop="address" label="地址"></el-table-column>
        <el-table-column label="操作" width="180">
          <template v-slot="scope">
            <el-button type="primary" size="small" @click="handleEdit(scope.row)">编辑</el-button>
            <el-button type="danger" size="small" @click="handleDelete(scope.row)">删除</el-button>
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
          { date: "2024-03-01", name: "张三", address: "北京市朝阳区" },
          { date: "2024-03-02", name: "李四", address: "上海市浦东新区" },
          { date: "2024-03-03", name: "王五", address: "广州市天河区" }
        ]
      };
    },
    methods: {
      handleEdit(row) {
        this.$message.info(`编辑 ${row.name}`);
      },
      handleDelete(row) {
        this.$confirm(`确定删除 ${row.name} 吗？`, "提示", {
          confirmButtonText: "确定",
          cancelButtonText: "取消",
          type: "warning"
        }).then(() => {
          this.tableData = this.tableData.filter(item => item !== row);
          this.$message.success("删除成功");
        }).catch(() => {
          this.$message.info("取消删除");
        });
      }
    }
  };
  </script>
  