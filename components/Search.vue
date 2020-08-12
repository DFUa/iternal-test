<template>
  <div class="search">
    <h1 class="search-header">Named Galaxies</h1>
    <input type="text" class="search-input" placeholder="Seacrh galaxies"
      @input="findGalaxyByName($event.target.value)">
  </div>
</template>

<script>
  export default {
    name: 'Search',
    data: () => ({
      timeout: null,
    }),
    methods: {
      findGalaxyByName(name) {
        clearTimeout(this.timeout);
        this.timeout = setTimeout(() => {
          this.$emit('search-galaxies', name)
        }, 100)
      }
    },
  }

</script>

<style lang="scss" scoped>
  .search {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 60px;

    .search-header {
      font-weight: 500;
      font-size: 34px;

      @media(max-width: 1000px) {
        width: 100%;
        text-align: center;
        margin-bottom: 15px;
      }
    }

    .search-input {
      border: 1px solid #E0E0E0;
      max-width: 270px;
      width: 100%;
      background: url(../assets/img/icons/search.svg) no-repeat center left 10px;
      padding: 10px;
      padding-left: 45px;
      border-radius: 4px;

      @media(max-width: 1000px) {
        margin: 0 auto;
      }
    }

    @media(max-width: 1000px) {
      flex-wrap: wrap;
    }

    @media(max-width: 800px) {
      margin-bottom: 25px;
    }
  }
</style>
