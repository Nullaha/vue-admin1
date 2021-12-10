<!-- POINTS: 左侧sidebar可能是路由组件<route-link>，可能是a标签<a>用于外链-->
<template>
  <component :is="type" :to="to">
    <slot />
  </component>
</template>

<script>
export default {
name:"Link",
props:{
  to:{
    type:String,
    required:true
  }
},
computed:{ 
  type(){
    return 'router-link'
  }
}
}
</script>

<style>

</style>