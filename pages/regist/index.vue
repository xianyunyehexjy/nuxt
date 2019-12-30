<template>
  <section class="container">
    <div class="login_logout">
      <h1>Login</h1>
      <div class="list">
        <el-form :model="ruleForm2" status-icon ref="ruleForm2" label-width="60px" class="demo-ruleForm">
          <el-form-item label="用户名" prop="userName">
            <el-input type="text" v-model="ruleForm2.userName" auto-complete="off"></el-input>
          </el-form-item>
          <el-form-item label="密码" prop="passWord">
            <el-input type="password" v-model="ruleForm2.passWord" auto-complete="off"></el-input>
          </el-form-item>
          <!-- <el-form-item label="验证">
            <div id="captcha">
              <p id="wait" v-if="!showJiyan" class="show"><i class="el-icon-loading"></i>正在加载验证码......</p>
            </div>
          </el-form-item> -->
          <el-form-item>
            <el-button type="primary" @click="regist" >注册</el-button>
           
          </el-form-item>
          <p class="username_pass">测试账号: 任意非空字符 密码: 123456</p>
        </el-form>
      </div>
    </div>
  </section>
</template>

<script>
  import Api from '~/utils/api'
  import Cookie from 'js-cookie'
  export default {
    head() {
      return {
        title: 'regist页面',
        meta: [
          { hid: 'description', name: 'description', content: 'regist页面....' }
        ] 
      }
    },
    data(){
      return {
        ruleForm2: {
          userName: '',
          passWord: ''
        },
        jiyanData: {
          geetest_challenge: '',
          geetest_validate: '',
          geetest_seccode: ''
        },
        showJiyan: false
      }
    },

    methods: {
      regist(formName) {
        Api.regist(this.ruleForm2)
              .then((res) => {
                Util.UI.toast('注册成功!', 'success')
              }).then((res) => {
                this.$router.push('/login')
              }, err => {
                 Util.UI.toast('注册失败!', 'error')
              })
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      }
    }
  }
</script>

<style scoped lang="scss">
  .container{
    -webkit-box-shadow: none;
    box-shadow: none;
    .login_logout{
      padding: 20px;
      border-radius: 5px;
      -webkit-box-shadow: 0 0 6px rgba(99, 99, 99, .4);
      box-shadow: 0 0 6px rgba(99, 99, 99, .4);
      width: 360px !important;
      /*height: 300px !important;*/
      margin-left: -180px;
      margin-top: -150px;
      position: absolute;
      left: 50%;
      top:50%;
      min-height: 300px;
    }
    .username_pass{
      font-size: 12px;
      color: #999;
      text-align: center;
    }
    #wait{
      line-height: 40px;
      color: #666;
    }
  }
  footer{
    display: none;
  }
</style>
