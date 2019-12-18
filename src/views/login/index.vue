<template>
  <div class="login">
    <!-- 放置一个卡片组件 -->
    <el-card class="login-card">
      <div class="title">
        <img src="../../assets/img/logo_index.png" alt />
      </div>
      <!-- 登录表单 表单容器 -->
      <el-form style="margin-top:30px">
        <!-- 表单域el-form-item=>一行 -->

        <el-form-item>
          <!-- 放置具体的组件 登录手机号-->
          <el-input placeholder="请输入手机号"></el-input>
        </el-form-item>
        <el-form-item>
          <!-- 表单域 -->
          <el-input style="width:70%" placeholder="请输入验证码"></el-input>
          <el-button plain>发送验证码</el-button>
         </el-form-item>
         <el-form-item>
           <el-checkbox>已经阅读用户隐私</el-checkbox>
         </el-form-item>
         <el-button type="primary" style="width:100%">登录</el-button>
      </el-form>
    </el-card>
  </div>
</template>

<script>
export default {}
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
