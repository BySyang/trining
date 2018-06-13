<template>
  	<div id="login">
			<section class="login mt-left pt-login">
		      <h1 class="login-h1">Hello!</h1>
		      <h2 class="login-h2 mt-4 mb-5">WELCOME TO MY WORLD!</h2>
		      <div class="input-group input-radius">
		        <img src="@/assets/img/user.png" class="mx-4 my-3 " width="25px" height="25px" alt="">
		        <input type="text" required="" pattern=".*[^ ].*" class="rm-input" placeholder="账号" v-model="logObj.user_code">
		      </div>
		
		      <div class="input-group input-radius mt-4">
		        <img src="@/assets/img/pwd.png" class="mx-4 my-3 " width="25px" height="25px" alt="">
		        <input type="password" required="" pattern=".*[^ ].*"  class="rm-input" placeholder="密码" v-model="logObj.password">
		      </div>
          <div class="btn-wrap">
             <button type="buttton" class="btn mt-5 btn_1" @click="login">登录</button>
          </div>
		    </section>
  	</div>
</template>

<script>
import qs from "querystring";
import "../assets/js/md5.min.js";
import crypto from "crypto";
export default {
  name: "",
  data() {
    return {
      logObj: {
        user_code: "",
        user_password: "",
        password:'',
      }
    };
  },
  methods: {
    login() {
      let self = this.logObj;
      var md5 = crypto.createHash("md5");
      md5.update(this.logObj.password);
      var user_password = md5.digest("hex");
      this.logObj.user_password = user_password.toUpperCase(); //英文全部转为大写
      this.$http
        .get(
          `user/login?user_code=${this.logObj.user_code}&user_password=${
            this.logObj.user_password
          }`
        )
        .then(res => {
          console.log(res);
        })
        .then(err => {
          console.log(err);
        });
    }
    // login(x) {
    //   var x = JSON.parse(x);
    //   if (x.Result) {
    //     localStorage.user0609 = JSON.stringify(x.Memory.user);
    //     localStorage.permission0609 = JSON.stringify(x.Memory.permission);
    //     this.$router.push("/home");
    //   } else {
    //     this.Prompt = x.Message;
    //     $("#login .modal_1").modal("show");
    //   }
    // }
  },
  created: function() {},
  mounted: function() {}
};
</script>

<style >
#login {
  height: 100vh;
  /*height: 100%;*/
  background: url(../assets/img/bg.png) right 50% no-repeat;
}
#login .btn_1 {
  width: 183px;
  height: 53px;
  background-image: linear-gradient(101deg, #17189d 0%, #3a3ce6 100%);
  font-family: MicrosoftYaHei;
  font-weight: normal;
  font-stretch: normal;
  line-height: 0px;
  font-size: 20px;
  letter-spacing: 2px;
  color: #ffffff;
  border-radius: 34px !important;
}
#login .btn-wrap {
  text-align: left;
  text-indent: 3em;
}
#login .pt-login {
  padding-top: 10% !important;
}
#login .mt-left {
  margin-left: 5% !important;
}
#login .input-radius {
  width: 322px;
  height: 52px;
  border: 0px;
  border: 0px;
  /* border: 1px solid #bbb; */
  background-color: #f7f5fb;
  border-radius: 34px;
  outline: none;
  margin-bottom: 20px;
  text-align: left;
  text-indent: 2em;
  line-height: 50px;
}
#login .rm-input {
  border: 0px;
  background-color: #f7f5fb;
  outline: none;
}
#login .login-h1 {
  font-family: ArialMT;
  font-size: 64px;
  line-height: 43px;
  text-align: left;
  margin-bottom: 20px;
  /* letter-spacing: 0px; */
  color: #404040;
}
#login .login-h2 {
  font-family: ArialMT;
  font-size: 24px;
  line-height: 43px;
  text-align: left;
  margin-bottom: 20px;
  /* letter-spacing: 0px; */
  color: #4d4d4d;
}
</style>
