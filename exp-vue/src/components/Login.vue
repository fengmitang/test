<template>
  <body id="poster">
  <h1 class='hcqFont hcqStyle1'>二手书交易平台</h1>
  <el-form class="login-container" label-position="left"
           label-width="0px">
    <h3 class="login_title">系统登录</h3>
    <el-form-item>
      <el-input type="text" v-model="loginForm.username"
                auto-complete="off" placeholder="账号"></el-input>
    </el-form-item>
    <el-form-item>
      <el-input type="password" v-model="loginForm.password"
                auto-complete="off" placeholder="密码"></el-input>
    </el-form-item>
    <el-form-item style="width: 100%">
      <el-button type="primary" style="width: 100%;background: #112b57;border: none" v-on:click="login">登录</el-button>
    </el-form-item>
  </el-form>
  </body>
</template>

<script>

export default {
  name: 'Login',
  data () {
    return {
      loginForm: {
        username: 'admin',
        password: '123'
      },
      responseResult: []
    }
  },
  methods: {
    login () {
      var _this = this
      console.log(this.$store.state)
      this.$axios
        .post('/login', {
          username: this.loginForm.username,
          password: this.loginForm.password
        })
        .then(successResponse => {
          if (successResponse.data.code === 200) {
            // var data = this.loginForm
            _this.$store.commit('login', _this.loginForm)
            var path = this.$route.query.redirect
            this.$router.replace({path: path === '/' || path === undefined ? '/index' : path})
          }
        })
        .catch(failResponse => {
        })
    }
  }
}
</script>

<style>

p{
  font-size: 100px;
  font-family: 微软雅黑;
  /*font-style: italic;*/
  color:rgb(46, 30, 171);
  text-align: center;
  font-weight: bold;
}
.hcqFont{position:relative;letter-spacing:.07em;font-size:3em;font-weight:normal;margin:0 auto}
.hcqFont:before,.hcqFont:after{position:absolute;top:0;left:0;right:0}
.hcqStyle1{
  font-size: 60px;
  text-align: center;
  color:rgb(59, 45, 100);
  text-shadow:0 0 1px currentColor,/*highlight*/-1px -1px 1px rgb(82, 62, 235),0 -1px 1px rgb(24, 10, 131),1px -1px 1px rgb(53, 191, 209),/*light shadow*/1px 1px 1px hsl(184,80%,10%),0 1px 1px hsl(184,80%,10%),-1px 1px 1px hsl(184,80%,10%),/*outline*/-2px -2px 1px hsl(184,80%,15%),-1px -2px 1px hsl(184,80%,15%),0 -2px 1px hsl(184,80%,15%),1px -2px 1px hsl(184,80%,15%),2px -2px 1px hsl(184,80%,15%),2px -1px 1px hsl(184,80%,15%),2px 0 1px hsl(184,80%,15%),2px 1px 1px hsl(184,80%,15%),-2px 0 1px hsl(184,80%,15%),-2px -1px 1px hsl(184,80%,15%),-2px 1px 1px hsl(184,80%,15%),/*dark shadow*/2px 2px 2px hsl(184,80%,5%),1px 2px 2px hsl(184,80%,5%),0 2px 2px hsl(184,80%,5%),-1px 2px 2px hsl(184,80%,5%),-2px 2px 2px hsl(184,80%,5%)}

#poster {
  background:url("../assets/Second.jpg") no-repeat;
  background-position: center;
  height: 100%;
  width: 100%;
  background-size: cover;
  position: fixed;
}
body{
  margin: 0px;
}
.login-container {
  border-radius: 15px;
  background-clip: padding-box;
  margin: 90px auto;
  width: 350px;
  padding: 35px 35px 15px 35px;
  background: #fff;
  border: 1px solid #eaeaea;
  box-shadow: 0 0 25px #cac6c6;
}
.login_title {
  margin: 0px auto 40px auto;
  text-align: center;
  color: #13487c;
}

</style>
