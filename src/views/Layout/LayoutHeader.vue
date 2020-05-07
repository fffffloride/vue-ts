<template>
  <div class="layout-header">
    <el-row>
      <el-col :xs="10" :sm="12" :md="14" :lg="16" :xl="18">
        <div class="system-info">
          <img class="logo" src="@/assets/logo.png" alt="" />
          <span class="title">后台管理系统</span>
        </div>
      </el-col>
      <el-col :xs="14" :sm="12" :md="10" :lg="8" :xl="6">
        <el-dropdown class="system-user" @command="userCommand">
          <span class="userinfo-inner">
            <img :src="require('@/assets/' + getUser.key + '.jpg')" alt="">
            {{getUser.username}}
          </span>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item command="usercenter">个人中心</el-dropdown-item>
            <el-dropdown-item divided command="logout">注销登录</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </el-col>
    </el-row>
  </div>
</template>

<script lang="ts">
// 引入装饰器
import { Component, Vue } from 'vue-property-decorator'
import { State, Action, Mutation, Getter } from 'vuex-class'
@Component({
  components: {}
})
export default class LayoutHeader extends Vue {
  @Getter("user") getUser: any;
  userCommand(command: String) :void{
    if (command === 'logout') {
      localStorage.removeItem("tsToken");
      this.$router.replace("/login");
    }
    if (command === 'usercenter') this.$router.push("/user");
  }
  created() {

  }
}
</script>

<style lang="scss" scoped>
.layout-header {
  height: 64px;
  line-height: 64px;
  background: #495060;
}
.system-info {
  text-align: left;
  .logo {
    position: relative;
    float: left;
    width: 40px;
    height: 40px;
    margin-top: 12px;
    margin-right: 10px;
    margin-left: 20px;
    border-radius: 50px;
  }
  .title {
    font-size: 18px;
    font-weight: bold;
    line-height: 64px;
    color: azure;
  }
}
.system-user {
  float: right;
  padding-right: 16px;
  text-align: right;
  .userinfo-inner {
    font-size: 16px;
    color: #fff;
    cursor: pointer;
    img {
      float: right;
      width: 40px;
      height: 40px;
      margin: 10px 0 10px 10px;
      border-radius: 20px;
    }
  }
}
</style>

