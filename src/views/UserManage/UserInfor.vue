<template>
  <div class="user-info">
    <div class="img-box">
      <h2 class="title">About me</h2>
      <img :src="require('@/assets/' + getUser.key + '.jpg')" alt />
      <h4>{{getUser.username}}</h4>
    </div>
    <div class="info-box">
      <h2 class="title">Acount</h2>
      <!-- form -->
      <el-form :model="userData" class="form-box">
        <el-form-item label="用户名">
          <el-input v-model="getUser.username" readonly></el-input>
        </el-form-item>
        <el-form-item label="密码">
          <el-input v-model="userData.pwd" type="password"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button
            @click="onSubmit"
            type="button"
            :loading="loading"
            :disabled="!userData.pwd"
          >修改密码</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script lang="ts">
// 引入装饰器
import { Component, Vue, Provide } from "vue-property-decorator";
import { Getter } from "vuex-class";
@Component({
  components: {}
})
export default class UserInfor extends Vue {
  @Getter("user") getUser: any;
  @Provide() userData: { username: String; pwd: String } = {
    username: "",
    pwd: ""
  };
  @Provide() loading: boolean = false;

  onSubmit() {
    // 发起请求
    (this as any).$axios
      .post("/api/users/changePwd", this.userData)
      .then((res: any) => {
        this.loading = false;
        this.$message({
          message: res.data.msg,
          type: "success"
        });
      })
      .catch(() => {
        this.loading = false;
      });
  }
}
</script>

<style lang="scss" scoped>
.user-info {
  display: flex;
  height: calc(100% - 70px);
  overflow: auto;
  color: #606266;
  .img-box,
  .info-box {
    height: 100%;
    padding: 20px;
    background: #fff;
    border: 1px solid #dcdfe6;
    box-sizing: border-box;
    .title {
      padding: 10px;
      margin-bottom: 20px;
      font-size: 16px;
      font-weight: bold;
      text-align: left;
      border-bottom: 1px solid #dcdfe6;
    }
  }
  .img-box {
    width: 30%;
    margin-right: 10px;
    text-align: center;
    img {
      width: 120px;
      height: 120px;
      border-radius: 50%;
    }
    h4 {
      margin-top: 20px;
      font-size: 16px;
    }
  }
  .info-box {
    flex: 1;
    .form-box {
      padding: 10px;
    }
  }
}
</style>

