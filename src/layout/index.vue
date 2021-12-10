<template>
  <div class="app-wrapper">
    <sidebar class="sidebar-container"/>
    <div style="margin-left:210px">
      <navbar />
      <!-- <tags-view /> -->
      <app-main />
    </div>
  </div>
</template>

<script>
import { Sidebar,Navbar,TagsView, AppMain } from "./components";

export default {
  name: "Layout",
  components: {
    Sidebar,Navbar,TagsView,AppMain,
    
  },
  
    Navbarcomputed: {
    sidebar() {
      return this.$store.state.app.sidebar;
    },
    device() {
      return this.$store.state.app.device;
    },
    fixedHeader() {
      return this.$store.state.settings.fixedHeader;
    },
    classObj() {
      return {
        hideSidebar: !this.sidebar.opened,
        openSidebar: this.sidebar.opened,
        withoutAnimation: this.sidebar.withoutAnimation,
        mobile: this.device === "mobile",
      };
    },
  },
  methods: {
    handleClickOutside() {
      this.$store.dispatch("app/closeSideBar", { withoutAnimation: false });
    },
  },
};
</script>

<style lang="scss" scoped>
@import "~@/styles/mixin.scss";
@import "~@/styles/variables.scss";
.app-wrapper{
  position: relative;
  height: 100%;
  width: 100%;
}


</style>
