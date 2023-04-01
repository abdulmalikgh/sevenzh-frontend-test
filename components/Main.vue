<template>
    <div
      class="main"
    >
      <Header @handleShowSideBar="$emit('handleShowSideBar')" />
      <MainTitle />
      <MainCard />
    </div>
</template>
  
  <script>
  export default {
    name: 'SideBar',
  }
  </script>