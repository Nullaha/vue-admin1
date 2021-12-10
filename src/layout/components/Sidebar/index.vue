<template>
  <el-menu>
    <sidebar-item v-for="route in routes" :key="route.path" :item="route" :base-path="route.path" />
  </el-menu>
</template>

<script>
import SidebarItem from './SidebarItem.vue';
export default {
  components: { SidebarItem },
  computed:{
    routes(){
      return this.$router.options.routes
    }
  }

};
</script>
