<template>
    <div class="login-wrap">
        <div class="ms-title">后台管理系统</div>
        <div class="ms-login">
            <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="0px" class="demo-ruleForm">
                <el-form-item prop="account">
                    <el-input v-model="ruleForm.account" placeholder="account"></el-input>
                </el-form-item>
                <el-form-item prop="password">
                    <el-input type="password" placeholder="password" v-model="ruleForm.password"></el-input>
                </el-form-item>
                <div class="login-btn">
                    <el-button type="primary" @click.native.prevent="handleLogin">登录</el-button>
                </div>
                <!--<p style="font-size:12px;line-height:30px;color:#999;">Tips : 用户名和密码随便填。</p>-->
            </el-form>
        </div>
    </div>
</template>

<script>
    export default {
        data: function(){
            return {
                ruleForm: {
                    account: '',
                    password: ''
                },
                rules: {
                    username: [
                        { required: true, message: '请输入用户名', trigger: 'blur' }
                    ],
                    password: [
                        { required: true, message: '请输入密码', trigger: 'blur' }
                    ]
                }
            }
        },
        methods: {

            handleLogin(){
                var that=this;
                this.$refs.ruleForm.validate((vaild)=>{
                    if(vaild){
                        var account=this.ruleForm.account;
                        var password=this.ruleForm.password;
                        var params = new URLSearchParams();
                        params.append('account',account);
                        params.append('password',password);
                        this.$axios.post('http://127.0.0.1:29357/GDHQ/public/index.php/index/index/login',params).then((res)=>{
                            console.log(res.data.name);
//                            console.log(2222);
                            if(res.data.code==1){
                                that.$message({
                                    message:'登录成功',
                                    type:'success'
                                });
                                setTimeout(()=>{
//                                    sessionStorage.setItem('access-user', JSON.stringify(res.data));
//                                    console.log(that.$router);
                                    localStorage.setItem('ms_username',res.data.name);
                                    that.$router.push("/dashboard");

                                },1500);

                                console.log('ok');
                            }else{
                                that.$message({
                                    message:res.data.msg+'',
                                    type:'warning'
                                })
                                console.log('no');
                            }
                        })
                    }else{
                        console.log('检查格式！')
                        return false;
                    }
                })
            },


        }
    }
</script>

<style scoped>
    .login-wrap{
        position: relative;
        width:100%;
        height:100%;
    }
    .ms-title{
        position: absolute;
        top:50%;
        width:100%;
        margin-top: -230px;
        text-align: center;
        font-size:30px;
        color: #fff;

    }
    .ms-login{
        position: absolute;
        left:50%;
        top:50%;
        width:300px;
        height:160px;
        margin:-150px 0 0 -190px;
        padding:40px;
        border-radius: 5px;
        background: #fff;
    }
    .login-btn{
        text-align: center;
    }
    .login-btn button{
        width:100%;
        height:36px;
    }
</style>