<template>
    <div>
        <el-table :data="paginatedData" border style="width: 100%">
            <el-table-column v-for="(head, index) in tableHead" :key="index" :label="head">
                <template v-slot="scope">
                    <el-input v-if="editingCell[scope.$index]?.[index]" v-model="tableData2[scope.$index][index]" size="mini" ref="inputRefs"
                        @blur="disableEdit(scope.$index, index)">
                    </el-input>
                    <span v-else @dblclick="enableEdit(scope.$index, index)">
                        {{ scope.row[index] }}
                    </span>
                </template>
            </el-table-column>
        </el-table>
        <!-- 分页组件 -->
        <el-pagination
            @current-change="handlePageChange"
            :current-page="currentPage"
            :page-size="pageSize"
            :total="tableData2.length"
            layout="prev, pager, next"
        />
    </div>
</template>

<script>
export default {
    data() {
        return {
            // 表格数据（二维数组）
            tableData2: [
                ["2024-03-01", "张三", "北京市朝阳区"],
                ["2024-03-02", "李四", "上海市浦东新区"],
                ["2024-03-03", "王五", "广州市天河区"],
                ["2024-03-01", "张三22", "北京市朝阳区"],
                ["2024-03-02", "李四22", "上海市浦东新区"],
                ["2024-03-03", "王五22", "广州市天河区"]
            ],
            // 表头
            tableHead: ["日期", "姓名", "地址"],
            // 记录编辑状态的对象
            editingCell: {}, // 形如 { 0: { 1: true } } 表示第0行第1列处于编辑模式
            currentPage: 1, // 当前页
            pageSize: 2 // 每页行数
        };
    },
    computed: {
        // 根据当前页和每页行数计算出当前页面的数据
        paginatedData() {
            const start = (this.currentPage - 1) * this.pageSize;
            const end = start + this.pageSize;
            return this.tableData2.slice(start, end);
        }
    },
    methods: {
        enableEdit(rowIndex, colIndex) {
            if (!this.editingCell[rowIndex]) {
                this.$set(this.editingCell, rowIndex, {});
            }
            this.$set(this.editingCell[rowIndex], colIndex, true);
            this.$nextTick(() => {
                const input = this.$refs.inputRefs?.[0]?.$el.querySelector("input");
                if (input) input.focus();
            });
        },
        disableEdit(rowIndex, colIndex) {
            if (this.editingCell[rowIndex]) {
                this.$set(this.editingCell[rowIndex], colIndex, false);
            }
            console.log(this.tableData2);
        },
        // 切换分页
        handlePageChange(newPage) {
            this.currentPage = newPage;
        }
    }
};
</script>