<template>
    <div>
        <el-table
            :data="tableData"
            style="width: 100%">
            <el-table-column
                prop="date"
                label="日期"
                width="180">
            </el-table-column>
            <el-table-column
                prop="name"
                label="姓名"
                width="180">
            </el-table-column>
            <el-table-column
                prop="address"
                label="地址">
            </el-table-column>
            <el-table-column label="操作">
                <template slot-scope="scope">
                    <el-button @click="copyText" class="copy_btn" :data-clipboard-text="scope.row.date + ' ' + scope.row.name + ' ' + scope.row.address">复制本行文字</el-button>
                </template>
            </el-table-column>
        </el-table>
    </div>
</template>

<script>
    import ClipboardJS from 'clipboard'

    export default {
        data() {
            return {
                tableData: [{
                    date: '2016-05-02',
                    name: '王小虎',
                    address: '上海市普陀区金沙江路 1518 弄'
                }, {
                    date: '2016-05-04',
                    name: '王小虎',
                    address: '上海市普陀区金沙江路 1517 弄'
                }, {
                    date: '2016-05-01',
                    name: '王小虎',
                    address: '上海市普陀区金沙江路 1519 弄'
                }, {
                    date: '2016-05-03',
                    name: '王小虎',
                    address: '上海市普陀区金沙江路 1516 弄'
                }]
            }
        },
        methods: {
            copyText () {
                let clipboard = new ClipboardJS('.copy_btn')

                clipboard.on('success', e => {
                    console.log(e)
                    // console.info('Action:', e.action)
                    console.info('Text:', e.text)
                    // console.info('Trigger:', e.trigger)
                    this.$message.success('复制成功')
                    e.clearSelection()
                    clipboard.destroy();
                })

                clipboard.on('error', e => {
                    // console.error('Action:', e.action)
                    // console.error('Trigger:', e.trigger)
                    this.$message.error('复制失败')
                    clipboard.destroy();
                })
            },
        }
    }
</script>

<style scoped>

</style>
