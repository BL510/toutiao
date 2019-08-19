<template>
  <div class="login">
    <el-card class="login-card">
      <div calss="title">
        <img src="../../assets/img/logo_index.png" alt />
      </div>
      <el-form :model="formData" :rules="rules">
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
        <el-form-item>
          <el-button @click="login" type="primary" style="width:100%">登录</el-button>
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>

<script>
export default {
  data () {
    var func = function (rule, value, callback) {
      if (value) {
        // 满足校验
      } else {
        // 不满足校验
        callback(new Error('您必须同意协议'))
      }
    }
    return {
      //   定义表单数据对象
      formData: {
        mobile: '',
        code: '',
        check: false
      },
      rules: {
        mobile: [
          {
            required: true,
            message: '手机号不能为空'
          },
          {
            pattern: /^1[3456789]\d{9}$/,
            message: '手机号格式错误'
          }
        ],
        code: [
          {
            required: true,
            message: '验证码不能为空',
            trigger: 'blur'
          },
          {
            pattern: /^\d{6}$/,
            message: '验证码长度必须为6个数字'
          }
        ],
        check: [{
        //   message: '无条件同意',
          validator: func
        }]
      }
    }
  },
  methods: {
    login () {
      //   validate手动验证表单数据
      this.$refs.loginFrom.validator(isOk => {
        if (isOk) {
          this.$axios({
            method: 'post',
            url: '/authorizations',
            data: this.formData
          }).then(result => {
            console.log(result.data.data)
          })
        }
      })
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
  display: flex;
  justify-content: center;
  align-items: center;
  .login-card {
    width: 400px;
    height: 330px;
    img {
      display: block;
      width: 200px;
      margin: 10px auto;
    }
  }
}
</style>
