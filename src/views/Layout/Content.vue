<template>
  <el-container class="layout-content">
    <!-- 左侧菜单 -->
    <el-aside width="200px">
      <slot name="left"></slot>
    </el-aside>
    <!-- 右侧页面 -->
    <el-main>
      <div class="top">
        <i class="fa fa-reorder"></i>
        <el-breadcrumb class="breadcrumb" separator="/">
          <el-breadcrumb-item
            v-for="(item, index) in breadCrumbItems"
            :key="index"
            :to="{path:item.path}"
          >{{item.title}}</el-breadcrumb-item>
        </el-breadcrumb>
      </div>
      <div class="content">
        <slot name="content"></slot>
      </div>
    </el-main>
  </el-container>
</template>

<script lang="ts">
// 引入装饰器
import { Component, Vue, Provide, Watch } from "vue-property-decorator";
@Component({
  components: {}
})
export default class Content extends Vue {
  @Provide() breadCrumbItems: any; // 面包屑的数组

  @Watch("$route") handleRouteChange(to: any) {
    this.initBreadCrumbItems(to);
  }

  created() {
    this.initBreadCrumbItems(this.$route);
  }

  initBreadCrumbItems(router: any) {
    // 根路由
    let breadCrumbItems = [
      {
        path: "/",
        title: "后台管理系统"
      }
    ];

    for (const index in router.matched) {
      if (router.matched[index].meta && router.matched[index].meta.title) {
        breadCrumbItems.push({
          path: router.matched[index].path ? router.matched[index].path : "/",
          title: router.matched[index].meta.title
        });
      }
    }
    this.breadCrumbItems = breadCrumbItems;
  }
}
</script>

<style lang="scss" scoped>
.layout-content {
  width: 100%;
  height: 100%;
  .el-main {
    padding: 0;
    .top {
      display: flex;
      height: 54px;
      background: #fff;
      border-right: none;
      border-bottom: 1px solid #e6e6e6;
      align-items: center;
      i {
        padding-left: 16px;
        font-size: 20px;
        cursor: pointer;
      }
      .breadcrumb {
        padding-left: 16px;
      }
    }
    .content {
      height: calc(100% - 54px);
      padding: 10px;
      box-sizing: border-box;
    }
  }
}
</style>
