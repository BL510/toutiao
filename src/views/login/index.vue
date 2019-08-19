<template>
  <div class="login">
    <el-card class="login-card">
      <div calss="title">
        <img src="../../assets/img/logo_index.png" alt />
      </div>
      <el-form :model="formData">
        <el-form-item prop="mobile">
          <el-input v-model="formData.mobile" placeholder="请输入手机号"></el-input>
        </el-form-item>
        <el-form-item prop="code">
          <el-input v-model="formData.code" style="width:65%" placeholder="请输入验证码"></el-input>
          <el-button style="float:right">发送验证码</el-button>
        </el-form-item>
        <el-form-item prop="check">
          <el-checkbox v-model="formData.check">我已阅读并同意用户协议和隐私条款</el-checkbox>
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>

<script>
export default {
  data () {
    return {
      //   定义表单数据对象
      formData: {
        mobile: '',
        code: '',
        check: false
      },
      rules: {}
    }
  }
}
</script>

<style lang="less" scoped>
.login {
  width: 100%;
  height: 100vh;
  background-image: url("../../assets/img/login_bg.jpg");
  background-size: cover;
  display:flex;
  justify-content: center;
  align-items:center;
  .login-card{
     width:400px;
     height:330px;
     img{
         display:block;
         width:200px;
         margin:10px auto;
     }
  }
}

</style>
