<template>
    <div>
        <el-table :data="paginatedData" border style="width: 100%">
            <el-table-column v-for="(head, index) in tableHead" :key="index" :label="head">
                <template v-slot="scope">
                    <el-input v-if="editingCell[scope.$index]?.[index]" 
                              v-model="tableData2[scope.$index][index]" 
                              size="mini" 
                              ref="inputRefs"
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
            tableData2: [
                ["2024-03-01", "张三", "北京市朝阳区"],
                ["2024-03-02", "李四", "上海市浦东新区"],
                ["2024-03-03", "王五", "广州市天河区"],
                ["2024-03-04", "赵六", "深圳市南山区"],
                ["2024-03-05", "孙七", "杭州市西湖区"]
            ],
            tableHead: ["日期", "姓名", "地址"],
            editingCell: {},
            currentPage: 1, // 当前页
            pageSize: 2 // 每页行数
        };
    },
    computed: {
        // 计算当前页的数据
        paginatedData() {
            const start = (this.currentPage - 1) * this.pageSize;
            const end = start + this.pageSize;
            return this.tableData2.slice(start, end);
        }
    },
    methods: {
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
