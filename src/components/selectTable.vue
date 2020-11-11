<template>
    <div class="selectTable" ref="selectTable">
        <el-input v-model="agencyInfo.agencyName" @focus="selectTableFlag = true" :placeholder="hintMsg"></el-input>
        <div class="selectTableList" v-show="selectTableFlag">
            <el-table :data="selectTableData" border style="width: 100%;height: 283px;overflow-y: scroll;margin-bottom: 50px;" @row-click="getRowClick">
                <el-table-column
                        :prop="agencyInfo.codeItem"
                        header-align="center"
                        align="center"
                        :label="agencyInfo.code">
                </el-table-column>
                <el-table-column
                        :prop="agencyInfo.nameItem"
                        header-align="center"
                        align="center"
                        :label="agencyInfo.name">
                </el-table-column>
            </el-table>
            <el-pagination
                    background
                    @current-change="currentChangeHandle"
                    layout="prev, pager, next"
                    :current-page="page"
                    :total="totalPage">
            </el-pagination>
        </div>
    </div>
</template>
<script>
    export default {
        props:['selectTableData','totalPage','pageIndex','agencyInfo','hintMsg'],
        data(){
            return {
                selectTableFlag:false,
                page: this.pageIndex
            }
        },
        created(){
        },
        mounted(){
            this.closeClick()
        },
        methods:{
            getRowClick(row,column,event){
                console.log(row,column,event)
                // this.search = row[`${this.agencyInfo.nameItem}`]
                this.agencyInfo.agencyCode = row[`${this.agencyInfo.codeItem}`]
                this.agencyInfo.agencyName = row[`${this.agencyInfo.nameItem}`]
                this.selectTableFlag = false;
                console.log(Object.values(row))
            },
            closeClick(){
                document.addEventListener('click',(e) => {
                    if (this.$refs.selectTable){
                        let isTable = this.$refs.selectTable.contains(e.target)
                        if (!isTable){
                            this.selectTableFlag = false;
                        }
                    }
                })
            },
            // 当前页
            currentChangeHandle (val) {
                this.page = val
            },
        },
        watch:{
            agencyInfo(val){
                this.$emit('update:agencyInfo',val)
            },
            page(val){
                this.$emit('update:pageIndex',val)
            }
        }
    }
</script>
<style lang="scss" scoped>
    .selectTable{
        width: 100%;
        position: relative;
        .selectTableList{
            background: #ffffff;
            border: 1px solid #ebeef5;
            width: 100%;
            min-width: 500px;
            height: auto;
            position: absolute;
            left: 0;
            top: 40px;
            z-index: 99;
        }
    }
</style>