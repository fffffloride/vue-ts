<template>
  <div class="login-page">
    <div class="page-center">
      <div class="info">
        <div class="title">
          <img src="@/assets/logo.png" alt />
          <span>米修在线</span>
        </div>
        <div class="detail">
          <span>米修在线, 让每个人都有机会学习编程, 更有能力选择学习想要学习的课程!</span>
        </div>
      </div>
      <!-- 插槽 -->
      <div class="container">
        <slot name="container"></slot>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component({
  components: {}
})
export default class LayoutHeader extends Vue {}
</script>

<style lang="scss" scoped>
.login-page {
  width: 100%;
  height: 100%;
  background-image: url(../../assets/login-back.svg);
  background-position: center 110px;
  background-repeat: no-repeat;
  background-size: 100%;
  .page-center {
    position: absolute;
    top: 60px;
    right: 0;
    left: 0;
    width: 400px;
    height: 540px;
    margin: auto;
    .info {
      height: 150px;
      text-align: center;
      .title {
        display: flex;
        justify-content: center;
        align-items: Center;
        font-size: 32px;
        color: rgba(0, 0, 0, 0.85);
        font-family: "Myriad Pro", "Helvetica Neue", Arial, Helvetica,
          sans-serif;
        font-weight: 600;
        img {
          width: 200px;
          padding-bottom: 3px;
        }
      }
      .detail {
        margin-bottom: 40px;
        font-size: 14px;
        line-height: 1.5;
        color: rgba(0, 0, 0, 0.45);
      }
    }
    .container {
      padding: 35px 35px 15px;
      background: #fff;
      border: 1px solid #eaeaea;
      -webkit-border-radius: 5px;
      -moz-border-radius: 5px;
      border-radius: 5px;
      box-shadow: 0 0 25px #cac6c6;
      background-clip: padding-box;
    }
  }
}
</style>
