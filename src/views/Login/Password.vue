<template>
  <div class="password">
    <LoginHeader>
      <el-form slot="container">
        <div class="title">
          <h3>找回密码</h3>
        </div>
      </el-form>
    </LoginHeader>
  </div>
</template>

<script lang="ts">
// 引入装饰器
import { Component, Vue } from 'vue-property-decorator'
import LoginHeader from './LoginHeader.vue';

@Component({
  components: { LoginHeader }
})
export default class Password extends Vue{}
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