<template>
    <div>
        <el-table :data="tableData2" border>
            <!-- 动态渲染表头 -->
            <el-table-column v-for="(head, index) in tableHead" :key="index" :label="head">
                <template v-slot="scope">
                    <span v-if="!editingCell[scope.$index]?.[index]" @dblclick="enableEdit(scope.$index, index)">
                        {{ scope.row[index] }}
                    </span>
                    <el-input v-else v-model="tableData2[scope.$index][index]" size="mini" ref="inputRefs"
                        @blur="disableEdit(scope.$index, index)"
                        @keydown.enter.native="disableEdit(scope.$index, index)" />
                </template>
            </el-table-column>
        </el-table>
        <!-- 分页组件 -->
        <el-pagination @current-change="handlePageChange" :current-page="currentPage" :page-size="pageSize"
            :total="tableData2.length" layout="prev, pager, next" />
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
                ["2024-03-03", "王五", "广州市天河区"]
            ],
            // 表头
            tableHead: ["日期", "姓名", "地址"],
            // 记录编辑状态的对象
            editingCell: {}, // 形如 { 0: { 1: true } } 表示第0行第1列处于编辑模式
            currentPage: 1, // 当前页
            pageSize: 2 // 每页行数
        };
    },
    methods: {
        // 启用编辑模式
        enableEdit(rowIndex, colIndex) {
            if (!this.editingCell[rowIndex]) {
                this.editingCell[rowIndex] = {};
            }
            this.editingCell[rowIndex][colIndex] = true;
            this.$nextTick(() => {
                const input = this.$refs.inputRefs?.[0]?.$el.querySelector("input");
                if (input) input.focus();
            });
        },
        // 关闭编辑模式
        disableEdit(rowIndex, colIndex) {
            if (this.editingCell[rowIndex]) {
                this.$set(this.editingCell[rowIndex], colIndex, false);
            }
        },
        
        // 切换分页
        handlePageChange(newPage) {
            this.currentPage = newPage;
        }
    }
};
</script>