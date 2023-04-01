<template>
    <div class="main-header">
      <div class="open-side-bar-wrapper">
        <button class="open-side-bar" @click="$emit('handleShowSideBar')">
        <img src="../static/icons/bars.svg" />
      </button>
      </div>
      <div class="main-header-nav">
        <div class="text">
            Take a tour
        </div>
        <div class="icon">
            <img src="../static/icons/Group 744.svg" />
        </div>
        <div class="icon">
            <img src="../static/icons/Group 745.svg" />
        </div>
        <div class="icon">
            <img src="../static/icons/Ellipse 11.svg" />
        </div>
      </div>
    </div>
</template>
  
  <script>
  export default {
    name: 'MainHeader',
    data() {
      return {
        hideSideBar: true
      }
    }
  }
  </script>