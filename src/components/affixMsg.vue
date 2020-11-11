<template>
    <div class="affix">
        <el-form :model="zhi" ref="ruleForm" :rules="rules" label-width="180px" class="demo-ruleForm">
            <el-form-item :label="getName" prop="pass">
                <p>{{zhi.name}}</p>
            </el-form-item>
            <label class="upload" @click="uploadBtn($event)">
                <em class="el-icon-upload2"></em>
            </label>
            <input @change="uploadName" accept=".pdf,.PDF" style="display: none" type="file" :ref="attachmentId">
        </el-form>
    </div>
</template>

<script>
    export default {
        data(){
            return{
                attachmentId: 'attachment' + new Date().getTime(),
                rules: {
                    pass: [
                        {
                            required: this.zhi.vital,
                            message:'请上传文件',
                            trigger: 'chang',
                        }
                    ]
                },
            }
        },
        props: ['index','zhi','type','name'],
        computed:{
            getName(){
                if (this.name){
                    return this.zhi.text
                }else {
                    return this.index
                }
            }
        },
        methods:{
            uploadName() {
                var that = this;
                let AllupExt = '.pdf|.PDF';
                let extName = this.$refs[that.attachmentId].files[0].name.substring(this.$refs[that.attachmentId].files[0].name.lastIndexOf('.')).toLowerCase();
                if (AllupExt.indexOf(extName + '|') == '-1') {
                    this.$alert('文件格式不正确，请重现上传', '警告', {
                        confirmButtonText: '确定',
                    })
                    return;
                }
                let fd = new FormData();
                fd.append('file1', this.$refs[that.attachmentId].files[0]);
                fd.append('table', this.type);
                this.$http.post('/uploadFile.do', fd).then(res => {
                    if (res.data.code != 1){
                        this.$alert('文件上传失败', '提示', {
                            confirmButtonText: '确定',
                        })
                        return
                    }
                    this.zhi.filePath = res.data.filepath
                    this.zhi.fileSize = res.data.filesize
                    this.zhi.name = res.data.name
                    this.$message({
                        message: '文件上传成功',
                        type: 'success'
                    });
                    this.$forceUpdate();
                })
            },
            uploadBtn(e) {
                this.$refs[this.attachmentId].click()
            },
        },
        mounted(){
            // console.log(this.zhi)
        },
        watch:{
            zhi(val){
                this.$emit('update:zhi',val)
            },
        }
    }
</script>

<style lang="scss" scoped>
    .affix{
        width: 100%;
        p{
            margin: 0;
            padding: 0;
        }
    }
</style>