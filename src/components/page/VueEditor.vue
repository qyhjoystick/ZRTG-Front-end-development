<template>
    <el-table
            :data="tableData3"
            height="350"
            border
            style="width: 100%">
        <el-table-column
                prop="date"
                label="柜号"
                width="125">
        </el-table-column>
        <el-table-column
                prop="name"
                label="出现的问题"
                width="125">
        </el-table-column>

    </el-table>
</template>

<script>
    export default {
        data() {
            return {
                tableData3: [{
                    date: '2016-05-03',
                    name: '王小虎',
                }, {
                    date: '2016-05-02',
                    name: '王小虎',
                }, {
                    date: '2016-05-04',
                    name: '王小虎',
                }, {
                    date: '2016-05-01',
                    name: '王小虎',
                }, {
                    date: '2016-05-08',
                    name: '王小虎',
                }, {
                    date: '2016-05-06',
                    name: '王小虎',
                    address: '上海市普陀区金沙江路 1518 弄'
                }, {
                    date: '2016-05-07',
                    name: '王小虎',
                }]
            }
        }
    }
</script>