<template>
    <div>
        <el-table :data="tableData2" border style="width: 100%">
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
            editingCell: {} // 形如 { 0: { 1: true } } 表示第0行第1列处于编辑模式
        };
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
        }
    }
};
</script>