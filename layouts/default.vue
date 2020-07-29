<template>
  <div class="layout">
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
$color-primary: #263238;

.layout {
  &-content-wrapper {
    font-family: Roboto;
    margin-left: 270px;
    color: $color-primary;

    @media screen and (max-width: 480px) {
      display: flex;
      flex-direction: column;
      margin-left: 0;
      margin-top: 70px;
    }
  }
}
</style>
