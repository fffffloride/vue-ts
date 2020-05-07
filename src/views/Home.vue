<template>
  <div class="home">
    <div class="home-body">
      <h4 class="title">讓世界愛上中國造！</h4>
      <p class="des">learn what you want, and just do it!</p>
      <el-button @click="learn">進入學習</el-button>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
@Component({
  components: {}
})
export default class Home extends Vue {
  learn(): void {
    // 新窗口打开
    window.open(
      "https://ke.qq.com/course/list/%E7%B1%B3%E6%96%AF%E7%89%B9%E5%90%B4?tuin=c9304a42",
      "_blank"
    );
  }
}
</script>

<style lang="scss" scoped>
.home {
  width: 100%;
  height: 100%;
  background: url(../assets/bg.jpg) no-repeat;
  background-size: 100% 100%;
  .home-body {
    height: 100%;
    padding: 100px;
    color: #fff;
    text-align: center;
    background-color: rgba(0, 0, 0, 0.6);
    box-sizing: border-box;
    .title {
      font-size: 32px;
      font-weight: bold;
      line-height: 60px;
    }
    .des {
      margin: 40px 0;
      font-size: 18px;
    }
  }
}
</style>
