<template>
  <div class="password">
    <LoginHeader>
      <el-form
        slot="container"
        :model="ruleForm"
        :rules="rules"
        ref="ruleForm"
        label-position="left"
        label-width="0px"
      >
        <div class="title">
          <h3>找回密码</h3>
        </div>

        <el-form-item prop="username">
          <el-input type="text" v-model="ruleForm.username" autocomplete="off" placeholder="账号">
            <i slot="prefix" class="fa fa-user-o"></i>
          </el-input>
        </el-form-item>

        <el-form-item prop="email">
          <el-input type="text" v-model="ruleForm.email" autocomplete="off" placeholder="邮箱">
            <i slot="prefix" class="fa fa-envelope-o"></i>
          </el-input>
        </el-form-item>

        <el-form-item>
          <el-button
            @click.native.prevent="handleSubmit"
            type="primary"
            style="width:100%"
            :loading="loading"
          >确定</el-button>
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
export default class Password extends Vue {
  @Provide() loading: boolean = false; // 是否发送网络请求

  @Provide() ruleForm: { username: string; email: string } = {
    username: "",
    email: ""
  };

  @Provide() rules = {
    username: [{ required: true, message: "请输入账号", trigger: "blur" }],
    email: [
      {
        required: true,
        message: "请输入邮箱地址",
        trigger: "blur"
      },
      {
        type: "email",
        message: "请输入正确的邮箱地址",
        trigger: "blur,change"
      }
    ]
  };

  handleSubmit(): void {
    (this.$refs["ruleForm"] as any).validate((valid: boolean) => {
      if (valid) {
        this.loading = true;
        // 网络请求
        (this as any).$axios
          .post("/api/users/findPwd", this.ruleForm)
          .then((res: any) => {
            this.loading = false;
            this.$message({
              message: res.data.msg,
              type: 'success'
            })
          })
          .catch(() => {
            this.loading = false;
          });
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