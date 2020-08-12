<template>
  <div class="main-page">
    <Search @search-galaxies="fitlerGalaxies" />
    <Table :galaxies="galaxies" @sort-galaxy="sortGalaxiesByName" />
  </div>
</template>

<script>
  import Search from '../components/Search';
  import Table from '../components/Table';

  export default {
    components: {
      Search,
      Table,
    },

    data: () => ({
      galaxies: [],
    }),

    mounted() {
      this.fetchData()
    },

    methods: {
      async fetchData() {
        this.galaxies = await this.$axios.$get('/api', {
          headers: {
            'Content-Type': 'application/json'
          }
        })
      },

      fitlerGalaxies(name) {
        this.fetchData().then(() => {
          if (name) {
            this.galaxies = this.galaxies.filter(galaxy => {
              return galaxy.name.toLowerCase().includes(name)
            })
          }
        })
      },

      sortGalaxiesByName(asc) {
        this.galaxies = this.galaxies.sort((a, b) => {
          if (a.name > b.name) {
            return asc ? -1 : 1;
          } else {
            return asc ? 1 : -1;
          }
          return 0;
        })
      }
    },
  }

</script>

<style lang="scss" scoped>
  .main-page {
    width: 100%;
    padding: 70px 60px;

    @media(max-width: 1000px) {
      padding: 30px;
    }

    @media(max-width: 800px) {
      padding: 15px;
    }
  }
</style>
