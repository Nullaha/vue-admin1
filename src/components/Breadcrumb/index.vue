<template>
  <el-breadcrumb separator="/">
    <!-- <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
    <el-breadcrumb-item><a href="/">活动管理</a></el-breadcrumb-item>
    <el-breadcrumb-item>活动列表</el-breadcrumb-item> -->
    <el-breadcrumb-item v-for="(item,index) in levelList" :key="item.path">
      <span v-if="item.redirect==='noRedirect'||index==levelList.length-1">{{item.meta.title}}</span>
      <a v-else @click="handleLink(item)">{{item.meta.title}}</a>
    </el-breadcrumb-item>
  </el-breadcrumb>
</template>

<script>
import pathToRegexp from "path-to-regexp";

export default {
  data() {
    return {
      levelList: null,
    };
  },
  watch: {
    $route() {
      console.log("watch-$route");
      this.getBreadcrumb();
    },
  },
  created() {
    this.getBreadcrumb();
  },
  methods: {
    getBreadcrumb() {
      // console.log(this.$route);
      // only show routes with meta.title
      let matched = this.$route.matched.filter(
        (item) => item.meta && item.meta.title
      );
      const first = matched[0];

      this.levelList = matched.filter((item) => item.meta && item.meta.title);
    },
    handleLink(item){
      const {redirect,path}=item;
      if(redirect){
        this.$router.push(redirect)
        return 
      }
    }
  },
};
</script>

<style lang="scss" scoped>
</style>
