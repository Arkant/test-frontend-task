<template>
  <div class="sidebar" />
</template>

<script>
export default {
  name: 'SideBar'
}
</script>

<style lang="scss">
.sidebar {
  height: 100%;
  width: 270px;
  position: fixed;
  top: 0;
  left: 0;
  background-color: #F9FAFB;

  @media screen and (max-width: 480px) {
    height: 70px;
    width: 100%;
  }
}
</style>
