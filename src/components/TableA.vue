<template>
    <div>
        <el-table :data="paginatedData" border style="width: 100%">
            <el-table-column v-for="(head, index) in tableHead" :key="index" :label="head">
                <template v-slot="scope">
                    <el-input 
                        v-if="isEditing(scope.$index, index)"
                        v-model="tableData[scope.$index + (currentPage - 1) * pageSize][index]" 
                        size="mini" 
                        ref="inputRefs"
                        @blur="disableEdit(scope.$index, index)"
                    />
                    <span v-else @dblclick="enableEdit(scope.$index, index)">
                        {{ scope.row[index] }}
                    </span>
                </template>
            </el-table-column>
        </el-table>

        <!-- 分页 -->
        <el-pagination
            @size-change="handleSizeChange"
            @current-change="handlePageChange"
            :current-page="currentPage"
            :page-sizes="[2, 5, 10, 20]"
            :page-size="pageSize"
            :total="tableData.length"
            layout="total, sizes, prev, pager, next, jumper"
        />
    </div>
</template>

<script>
export default {
    data() {
        return {
            tableHead: ["日期", "姓名", "地址"], // 表头
            tableData: [ // 表格数据
                ["2024-03-01", "张三", "北京市朝阳区"],
                ["2024-03-02", "李四", "上海市浦东新区"],
                ["2024-03-03", "王五", "广州市天河区"],
                ["2024-03-04", "赵六", "深圳市南山区"],
                ["2024-03-05", "孙七", "杭州市西湖区"],
                ["2024-03-06", "周八", "南京市鼓楼区"],
                ["2024-03-07", "吴九", "成都市武侯区"],
                ["2024-03-08", "郑十", "重庆市渝中区"]
            ],
            editingCell: {}, // 记录当前正在编辑的单元格
            currentPage: 1, // 当前页码
            pageSize: 5 // 默认每页显示 5 条数据
        };
    },
    computed: {
        // 计算当前页的数据
        paginatedData() {
            const start = (this.currentPage - 1) * this.pageSize;
            return this.tableData.slice(start, start + this.pageSize);
        }
    },
    methods: {
        // 判断当前单元格是否处于编辑模式
        isEditing(rowIndex, colIndex) {
            const realIndex = rowIndex + (this.currentPage - 1) * this.pageSize;
            return this.editingCell[realIndex]?.[colIndex] === true;
        },
        // 启用编辑
        enableEdit(rowIndex, colIndex) {
            const realIndex = rowIndex + (this.currentPage - 1) * this.pageSize;

            // 初始化对象
            if (!this.editingCell[realIndex]) {
                this.$set(this.editingCell, realIndex, {});
            }

            this.$set(this.editingCell[realIndex], colIndex, true);

            // 等待 DOM 更新后再执行 focus()
            this.$nextTick(() => {
                const input = this.$refs.inputRefs?.[0]?.$el?.querySelector("input");
                if (input) {
                    input.focus();
                }
            });
        },
        // 关闭编辑模式
        disableEdit(rowIndex, colIndex) {
            const realIndex = rowIndex + (this.currentPage - 1) * this.pageSize;
            if (this.editingCell[realIndex]) {
                this.$set(this.editingCell[realIndex], colIndex, false);
            }
        },
        // 切换分页
        handlePageChange(newPage) {
            this.currentPage = newPage;
        },
        // 修改每页显示条数
        handleSizeChange(newSize) {
            this.pageSize = newSize;
            this.currentPage = 1;
        }
    }
};
</script>
