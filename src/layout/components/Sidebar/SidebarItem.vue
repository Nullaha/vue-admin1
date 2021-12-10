<template>
  <div v-if="!item.hidden">
    <template v-if="hasOneShowingChild(item.children, item)">
      <router-link :to="resolvePath(onlyOneChild.path)"><!-- <app-link> -->
        <el-menu-item :index="resolvePath(onlyOneChild.path)">
          <!-- <i class="el-icon-menu"
            :class="onlyOneChild.meta && onlyOneChild.meta.icon"
          ></i> -->
          <span slot="title">{{ onlyOneChild.meta.title }}</span>
        </el-menu-item> 
        </router-link><!-- </app-link> -->
    </template>

    <el-submenu v-else :index="resolvePath(item.path)">
      <template slot="title">
        <!-- <i class="el-icon-location"></i>
      <span slot="title">导航一</span> -->
        <!-- <i class="el-icon-menu" :class="item.meta && item.meta.icon"></i> -->
        <span slot="title">{{ item.meta.title }}</span>
      </template>
      <!-- 循环 -->
      <sidebar-item
        v-for="child in item.children"
        :key="child.path"
        :item="child"
        :base-path="resolvePath(child.path)"
      />
    </el-submenu>
  </div>
</template>

<script>
import path from "path";
import { isExternal } from "@/utils/validate";
import AppLink from "./Link.vue";
export default {
  name: "SidebarItem",
  components: { AppLink },
  props: {
    item: {
      type: Object,
      require: true,
    },
    basePath: {
      type: String,
      default: "",
    },
  },
  data() {
    this.onlyOneChild = null
    return {
      // onlyOneChild: null,
    };
  },
  methods: {
    hasOneShowingChild(children = [], parent) {
      debugger
      // const showingChildren = children.filter((item) => {
      //   return !item.hidden;
      // });
      const showingChildren = children.filter(item=>!item.hidden);

      // When there is only one child router, the child router is displayed by default
      if (showingChildren.length === 1) {
        this.onlyOneChild = children[0];
        return true;
      }

      //POINTS: Show parent if there are no child router to display
      if(showingChildren.length ===0){
        this.onlyOneChild = {...parent,path:''}
        return true
      }

      return false;
    },
    resolvePath(routePath) {
      console.log(routePath);
      if (isExternal(routePath)) {
        return routePath;
      }
      if (isExternal(this.basePath)) {
        return this.basePath;
      }
      return path.resolve(this.basePath, routePath);
    },
  },
};
</script>

<style>
</style>