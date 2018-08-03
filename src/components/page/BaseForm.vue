
 <template>
    <div>
        <div class="handle-box">

            <el-form ref="form" :model="form" :rules="rules2" label-width="80px">
                <el-row>
                    <!--<el-col :span="8">-->
                        <!--<div class="grid-content bg-purple">-->
                            <!--<el-form-item prop="status">-->
                                <!--<el-select v-model="form.status" placeholder="筛选状态" class="handle-select mr10" style="margin-left: 0px">-->
                                    <!--<el-option key="1" label="正常" value="0"></el-option>-->
                                    <!--<el-option key="2" label="异常" value="1"></el-option>-->
                                <!--</el-select>-->
                            <!--</el-form-item>-->
                        <!--</div>-->
                    <!--</el-col>-->
                    <el-col :span="8">
                        <div class="grid-content bg-purple">
                            <el-button type="primary" icon="search" @click="search('validatePass')">搜索</el-button>
                        </div>
                    </el-col>

                    <el-col :span="8">
                        <div class="grid-content bg-purple-light">
                            <el-form-item prop="date">
                                <el-date-picker
                                        v-model="form.date"
                                        type="date"
                                        placeholder="选择日期"
                                        format="yyyy 年 MM 月 dd 日"
                                        value-format="yyyy-MM-dd">
                                </el-date-picker>
                            </el-form-item>
                        </div>
                    </el-col>
                </el-row>
            </el-form>

        </div>

         <el-table
                 :data="tableData"
                 height="325"
                 border
                 style="width: 100%">
             <el-table-column
                     prop="no"
                     label="柜号"
                     width="180">
             </el-table-column>
             <el-table-column
                     prop="equipment"
                     label="设备"
                     width="180">
             </el-table-column>
             <el-table-column
                     prop="status"
                     label="状态">
             </el-table-column>
             <el-table-column
                     prop="place"
                     label="地点">
             </el-table-column>
         </el-table>
     </div>

</template>

<script>
    export default {
        data() {
            var validatePass = (rule, value, callback) => {
                if (this.form.date === '') {
                    callback(new Error('请选择日期'));
                } else {
                    callback();
                }
            };

            return {
                rules2: {
                    date: [
                        { validator: validatePass, trigger: 'blur' }
                    ]
                },
                form: {
                    status: '',
                    date: ''
                },
                allow:'',
                select_cate: '',
                select_word: '',
                tableData: [],

            }
        },
        created() {
            var that = this;
            var params = new URLSearchParams();

            params.append('code',0);
            this.$axios.post('http://127.0.0.1:29357/GDHQ/public/index.php/index/index/engine2',params).then((res)=>{
//                console.log(this.form);
                that.tableData = res.data;
            })

        },
        methods: {
            search() {
                if (this.form.date === '') {
                    alert('请选择日期');
                    return false;
                }
                var status = this.form.status;
                var date   = this.form.date;
                var params = new URLSearchParams();
                params.append('status',status);
                params.append('date',date);
                params.append('code',1);
                this.$axios.post('http://127.0.0.1:29357/GDHQ/public/index.php/index/index/engine2',params).then((res)=>{
                    this.tableData = res.data;
                });
            }
        }
    }


</script>

 <style scoped>
     .handle-box {
         margin-bottom: 20px;
     }

     .handle-select {
         width: 120px;
     }

     .handle-input {
         width: 300px;
         display: inline-block;
     }
     .del-dialog-cnt{
         font-size: 16px;
         text-align: center
     }
 </style>