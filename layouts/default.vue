<template>
  <el-container>
    <el-header style="padding-right: 0;padding-left: 0">
      <el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal" @select="handleSelect">
        <el-menu-item><nuxt-link to="/about">About</nuxt-link></el-menu-item>
        <el-menu-item><nuxt-link to="/news">News</nuxt-link></el-menu-item>
        <el-menu-item><nuxt-link to="/about/user">User</nuxt-link></el-menu-item>
      </el-menu>
    </el-header>

    <el-main>
      <nuxt/>
    </el-main>
    <el-footer style="color: #909399;text-align: center;font-size: 13px;line-height: 60px;height: 60px">©2018 大数据部
    </el-footer>
  </el-container>
</template>

<style>

</style>
