<template>
  <div>
    <el-table :data="pagedTableData" border style="width: 100%">
      <el-table-column prop="date" label="日期" width="180"></el-table-column>
      <el-table-column prop="name" label="姓名" width="180"></el-table-column>
      <el-table-column prop="address" label="地址"></el-table-column>
    </el-table>
    <el-pagination
      @current-change="handlePageChange"
      :current-page="currentPage"
      :page-size="pageSize"
      layout="prev, pager, next"
      :total="tableData.length">
    </el-pagination>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        { date: "2024-03-01", name: "张三", address: "北京市朝阳区" },
        { date: "2024-03-02", name: "李四", address: "上海市浦东新区" },
        { date: "2024-03-03", name: "王五", address: "广州市天河区" },
        { date: "2024-03-04", name: "赵六", address: "深圳市南山区" },
        { date: "2024-03-05", name: "孙七", address: "杭州市西湖区" }
      ],
      currentPage: 1,
      pageSize: 2
    };
  },
  computed: {
    pagedTableData() {
      const start = (this.currentPage - 1) * this.pageSize;
      return this.tableData.slice(start, start + this.pageSize);
    }
  },
  methods: {
    handlePageChange(page) {
      this.currentPage = page;
    }
  }
};
</script>
