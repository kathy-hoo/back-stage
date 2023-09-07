<template>
  <div class="home">
    <el-container>
      <el-header class="header">
        <el-row :gutter="20">
          <el-col :span="4"
            ><img src="../assets/logo.png" class="logo" alt=""
          /></el-col>
          <el-col :span="16"><h1>后台管理系统</h1></el-col>
          <el-col :span="4"><span>退出登录</span></el-col>
        </el-row>
      </el-header>
      <el-container>
        <el-aside width="200px">Aside</el-aside>
        <el-main>Main</el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({});
</script>

<style lang="scss" scoped>
.header {
  height: 80px;
  background: #666;
  .logo {
    height: 80px;
  }
  h1,
  span {
    line-height: 80px;
    text-align: center;
    height: 80px;
  }
}
</style>
