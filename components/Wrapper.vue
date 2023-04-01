<template>
  <div
    class="wrapper"
  >
      <SideBar v-if="showSideBar" @handleHideSide="handleHideSide"/>
      <Main @handleShowSideBar="handleShowSideBar"/>
  </div>
</template>

<script>
export default {
  name: 'PageWrapper',
  data() {
    return {
      showSideBar:true
    }
  },
  mounted() {
    window.addEventListener("resize", this.handleWindowResize);
  },
  unmounted() {
    window.removeEventListener("resize", this.handleWindowResize);
  },
  methods: {
    handleHideSide() {
      this.showSideBar = false
    },
    handleShowSideBar() {
      this.showSideBar = true
    },
    handleWindowResize(e) {
      if(window.innerWidth >= 992) {
        this.showSideBar = true
      } else {
        this.showSideBar = false
      }
    }
  }
}
</script>
