<template>
    <div style="width: 100%">
        <ul class="flow_chart">
            <li v-for="(item,i) in flowData.nodeList" :key="i"  :class="item.current ? 'history activation current': ((!item.current) && (item.auditHistorys === undefined || item.auditHistorys.length < 1)) ? '' : 'history activation'">
                <div>
                    <div :class="item.current?'yuan el-icon-check':'yuan'"></div>
                    <div class="jt"></div>
                    <span>{{item.elementName}}</span>
                </div>
            </li>
        </ul>
        <el-table
                :data="tableData"
                border
                v-loading="dataListLoading"
                style="width: 100%;">
            <el-table-column
                    type="index"
                    header-align="center"
                    align="center"
                    label="序号"
                    width="50">
            </el-table-column>
            <el-table-column
                    prop="taskName"
                    header-align="center"
                    align="center"
                    width="120"
                    label="任务名称">
            </el-table-column>
            <el-table-column
                    prop="userName"
                    header-align="center"
                    align="center"
                    width="150"
                    label="执行人姓名">
            </el-table-column>
            <el-table-column
                    prop="excuteDate"
                    header-align="center"
                    align="center"
                    width="180"
                    label="执行人时间">
            </el-table-column>
            <el-table-column
                    prop="phone"
                    header-align="center"
                    align="center"
                    width="180"
                    label="联系方式">
            </el-table-column>
            <el-table-column
                    prop="auditMsg"
                    header-align="center"
                    align="center"
                    label="审核意见">
            </el-table-column>
        </el-table>
    </div>
</template>
<script>
    export default {
        props:['flowData','tableData'],
        data() {
            return {
                dataListLoading:false,
            };
        },
        methods: {},
    };
</script>
<style lang="scss">
    ul{
        list-style: none;
    }
    .flow_chart{
        height: 100px;
        margin: 10px 0 22px;
        display: flex;
        justify-content: space-evenly;
        li{
            width: 100%;
            position: relative;
            height: 50px;
            margin-top: 30px;
            &>div{
                width: 120px;
                height: 50px;
                border: 1px #BFBFBF solid;
                border-radius: 5px;
                background: #fff;
                position: absolute;
                left: 50%;
                top: 50%;
                transform: translate(-50%, -50%);
                z-index: 10;
                span{
                    display: block;
                    width: 100px;
                    position: absolute;
                    left: 50%;
                    top: 50%;
                    transform: translate(-50%, -50%);
                    color: #666666;
                    text-align: center;
                    cursor: default;
                }
                .jt{
                    position: absolute;
                    left: 50%;
                    top: -10px;
                    margin-left: -10px;
                    display: block;
                    width: 0;
                    height: 0;
                    border-width: 0 10px 10px;
                    border-style: solid;
                    border-color: transparent transparent #BFBFBF;
                    &:before{
                        content: '';
                        position: absolute;
                        left: 50%;
                        top: 1px;
                        margin-left: -9px;
                        display: block;
                        width: 0;
                        height: 0;
                        border-width: 0 9px 9px;
                        border-style: solid;
                        border-color: transparent transparent #fff;
                    }
                }
                .yuan{
                    position: absolute;
                    top: -42px;
                    left: 50%;
                    margin-left: -12px;
                    width: 24px;
                    height: 24px;
                    background: #fff;
                    border: 2px #BFBFBF solid;
                    border-radius: 50%;
                }
            }
            &:after{
                content: '';
                width: 50%;
                height: 2px;
                position: absolute;
                left: 0;
                top: -30px;
                background: #BFBFBF;
            }
            &:before{
                content: '';
                width: 50%;
                height: 2px;
                position: absolute;
                left: 50%;
                top: -30px;
                background: #BFBFBF;
            }
            &.history{
                &>div{
                    border: 1px #004798 solid;
                    span{
                        color: #004798;
                    }
                    .jt{
                        border-color: transparent transparent #004798;
                    }
                    .yuan{
                        border: 2px #004798 solid;
                    }
                }
                &:after{
                    background: #004798;
                }
                &:before{
                    background: #004798;
                }
                &.last{
                    &:before{
                        background: #BFBFBF;
                    }
                }
            }
            &.activation{
                &>div{
                    border: 1px #004798 solid;
                    span{
                        color: #004798;
                    }
                    .jt{
                        border-color: transparent transparent #004798;
                    }
                    .yuan{
                        border: 2px #004798 solid;
                    }
                }
                &:after{
                    background: #004798;
                }
                &:before{
                    background: #004798;
                }
            }
            &.current{
                &>div{
                    background: #004798;
                    span{
                        color: #fff;
                    }
                    .jt{
                        &:before{
                            display: none;
                        }
                    }
                    .yuan{
                        background: #004798;
                        color: #fff;
                        &:before{
                            position: absolute;
                            left: 50%;
                            top: 50%;
                            transform: translate(-50%, -50%);
                        }
                    }
                }
            }
        }
    }

</style>