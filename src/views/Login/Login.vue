<template>
  <div class="login">
    <LoginHeader>
      <el-form
        :rules="rules"
        :model="ruleForm"
        ref="ruleForm"
        label-position="left"
        label-width="0px"
        slot="container"
      >
        <div class="title">
          <h3>账号密码登录</h3>
        </div>
        <!-- username -->
        <el-form-item prop="username">
          <el-input type="text" v-model="ruleForm.username" auto-complete="off" placeholder="账号">
            <i slot="prefix" class="fa fa-user-o"></i>
          </el-input>
        </el-form-item>

        <!-- password -->
        <el-form-item prop="pwd">
          <el-input type="password" v-model="ruleForm.pwd" auto-complete="off" placeholder="密码">
            <i slot="prefix" class="fa fa-lock"></i>
          </el-input>
        </el-form-item>

        <!-- 登录button -->
        <el-form-item>
          <el-button
            :loading="isLogin"
            @click.native.prevent="handleSubmit"
            type="primary"
            style="width:100%;"
          >登录</el-button>
        </el-form-item>

        <!-- 7天登录和忘记密码 -->
        <el-form-item>
          <el-checkbox v-model="ruleForm.autoLogin" :checked="ruleForm.autoLogin">7天内自动登录</el-checkbox>
          <el-button @click="$router.push('/password')" type="text" class="forget">忘记密码？</el-button>
        </el-form-item>
      </el-form>
    </LoginHeader>
  </div>
</template>

<script lang="ts">
// 引入装饰器
import { Component, Vue, Provide } from "vue-property-decorator";
import LoginHeader from "./LoginHeader.vue";

@Component({
  components: { LoginHeader }
})
export default class Login extends Vue {
  @Provide() isLogin: boolean = false;
  @Provide() ruleForm: {
    username: String;
    pwd: String;
    autoLogin: boolean;
  } = {
    username: "",
    pwd: "",
    autoLogin: true
  };

  @Provide() rules = {
    username: [{ required: true, message: "请输入密码", trigger: "blur" }],
    pwd: [{ required: true, message: "请输入密码", trigger: "blur" }]
  };

  handleSubmit(): void {
    (this.$refs.ruleForm as any).validate((valid: boolean) => {
      if (valid) {
        console.log(1);
      }
    });
  }
}
</script>

<style lang="scss" scoped>
.title {
  margin: 0 auto 40px;
  color: #505458;
  text-align: center;
}

i {
  margin-left: 8px;
  font-size: 14px;
}
.forget {
  float: right;
}
</style>