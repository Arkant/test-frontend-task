<template>
  <div>
    <SideBar />
    <div class="layout-content-wrapper">
      <Nuxt />
    </div>
  </div>
</template>

<script>
import SideBar from '../components/SideBar'

export default {
  name: 'DefaultLayout',
  components: {
    SideBar
  }
}
</script>

<style lang="scss">
.layout-content-wrapper {
  font-family: Roboto;
  margin-left: 270px;
}
</style>
