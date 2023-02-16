<!--
 * @Description: 
 * @Author: JunLiangWang
 * @Date: 2023-02-15 22:15:23
 * @LastEditors: JunLiangWang
 * @LastEditTime: 2023-02-15 22:15:34
-->
<template>
  <div class="normal-page-container">
    <slot></slot>
  </div>
</template>

<script>
export default {
   name:'NormalPageContainer'
}
</script>

<style scoped>
.normal-page-container{
    margin: 120px;
}
</style>