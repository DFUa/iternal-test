<template>
  <aside></aside>
</template>

<script>
  export default {
    name: 'Sidebar',
  }

</script>

<style lang="scss" scoped>
  aside {
    width: 270px;
    min-height: 70px;
    flex-shrink: 0;
    background-color: #F9FAFB;

    @media(max-width: 1000px) {
      width: 200px;
    }

    @media(max-width: 800px) {
      width: 100%;
    }
  }
</style>
