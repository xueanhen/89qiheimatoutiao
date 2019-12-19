<template>
  <div class="login">
    <!-- 放置一个卡片组件 -->
    <el-card class="login-card">
      <div class="title">
        <img src="../../assets/img/logo_index.png" alt />
      </div>
      <!-- 登录表单 表单容器 el-form 需要绑定model属性 rules属性绑定验证规则对象 -->
      <el-form ref="myForm" style="margin-top:30px" :model="loginForm" :rules="loginRules">
        <!-- 表单域el-form-item=>一行    这里做校验的时候 要加上一个prop
        prop是要校验的字段名-->

        <el-form-item prop="mobile">
          <!-- 放置具体的组件 登录手机号-->
          <el-input v-model="loginForm.mobile" placeholder="请输入手机号"></el-input>
        </el-form-item>
        <el-form-item prop="code">
          <!-- 表单域 -->
          <el-input v-model="loginForm.code" style="width:70%" placeholder="请输入验证码"></el-input>
          <el-button plain>发送验证码</el-button>
        </el-form-item>
        <el-form-item prop="check">
          <el-checkbox v-model="loginForm.check">已经阅读用户隐私</el-checkbox>
        </el-form-item>
        <!-- 注册一个点击事件 -->
        <el-button @click="submitLogin" type="primary" style="width:100%">登录</el-button>
      </el-form>
    </el-card>
  </div>
</template>

<script>
export default {
  // 第一步 在data 中电仪表单数据对象
  data () {
    return {
      // 定义一个表单数据对象
      loginForm: {
        mobile: '',
        code: '',
        check: false
      },
      loginRules: {
        // 验证规则 验证登录表单的 key(字段名)：value(数组)
        mobile: [
          {
            required: true,
            message: '请输入你的手机号'
          },
          {
            pattern: /^1[3456789]\d{9}$/,
            message: '手机格式不正确'
          }
        ],
        code: [
          { required: true, message: '请输入您的验证码' },
          {
            pattern: /^\d{6}$/,
            message: '验证码格式不正确'
          }
        ],
        // 自定义函数
        check: [
          {
            validator: function (rule, value, callback) {
              // rule 当前的规则无用
              // value就是知道我们要校验的值 就是check的值
              //
              if (value) {
                // 认为校验通过 就过去
                callback()
              } else {
                // 认为校验不通过 要提示信息
                callback(new Error('您必须无条件同意被我们坑'))
              }
            }
          }
        ]
      }
    }
  },
  methods: {
    submitLogin () {
      // el-form实例
      this.$refs.myForm.validate((isOK) => {
        if (isOK) {
          // 认为前端校验登录表单成功
          // console.log('发送验证码到后台校验')
          // 地址参数(放在params对象) 查询参数
          // body参数 放在data对象里
          this.$axios({
            url: '/authorizations', // 请求地址
            method: 'post',
            data: this.loginForm // 直接用loginForm的数据
            // 请求后去哪里接收接口呢？
          })
            .then(result => {
              // 用then作为接收接口，请求成功之后才进入到then，失败后
              // 用catch()
              console.log(result)
            })
            .catch(error => {
              console.log(error)
            })
        }
      })
    }
  }
}
</script>

<style lang='less' scoped>
.login {
  background-image: url("../../assets/img/login_bg.jpg");
  height: 100vh;
  background-size: cover; //自适应背景
  display: flex;
  justify-content: center;
  align-items: center;
  .login-card {
    width: 440px;
    height: 350px;
    .title {
      text-align: center;
      img {
        height: 44px;
      }
    }
  }
}
</style>
