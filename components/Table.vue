<template>
  <div>
    <div class="table-view" v-if="galaxies && galaxies.length">
      <div class="table-head">
        <div class="table-row">
          <div class="table-col col-1" @click="sortGalaxiesByName">
            Galaxy Name
            <i :class="{'sort-direction': true, 'rotate': !asc}"></i>
          </div>
          <div class="table-col col-2">Constellation</div>
          <div class="table-col col-3">Origin of Name</div>
        </div>
      </div>
      <div class="table-body">
        <div class="table-row" v-for="galaxy in galaxies" :key="galaxy.id">
          <div class="table-col col-1" @click="sortGalaxiesByName">
            <p class="mobile-table-name">Galaxy Name</p>
            <div class="galaxy-name-img">
              <img :src="galaxy.img" :alt="galaxy.name">
            </div>
            {{galaxy.name}}
          </div>
          <div class="table-col col-2">
            <p class="mobile-table-name">Constellation</p>
            {{galaxy.constellation}}
          </div>
          <div class="table-col col-3">
            <p class="mobile-table-name">Origin of Name</p>
            {{galaxy.originOfName}}
          </div>
        </div>
      </div>
    </div>
    <div class="no-data" v-else>
      <h2>No Data</h2>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Table',
    props: {
      galaxies: Array,
    },
    data: () => ({
      asc: false,
    }),
    methods: {
      sortGalaxiesByName() {
        this.asc = !this.asc
        this.$emit('sort-galaxy', this.asc)
      }
    },
  }

</script>

<style lang="scss" scoped>
  .table-view {
    .table-head {
      text-transform: uppercase;
      font-size: 12px;
      font-weight: 900;
      letter-spacing: 1px;
      margin-bottom: 15px;

      .table-col {
        .sort-direction {
          margin-left: 10px;
          width: 10px;
          height: 10px;
          background: url(~assets/img/icons/arrow.svg) center center no-repeat;
          display: none;
          transition: all .3s;

          &.rotate {
            transform: rotate(180deg);
          }
        }

        &:hover {
          .sort-direction {
            display: inline-block;
          }
        }
      }

      .col-1 {
        cursor: pointer;
      }

      @media(max-width: 800px) {
        display: none;
      }
    }

    .table-body {
      .table-row {
        border: 1px solid #E0E0E0;
        transition: all .3s;

        .table-col {
          &+.table-col {
            border-left: 1px solid #E0E0E0;
          }

          @media(max-width: 800px) {
            width: 100%;
            padding: 10px;

            &+.table-col {
              border-left: none;
              border-top: 1px solid #E0E0E0;
            }
          }
        }

        &+.table-row {
          border-top: none;
        }

        &:hover {
          background-color: rgba(97, 128, 239, 0.2);

          .table-col {
            border-color: transparent;
          }
        }

        @media(max-width: 800px) {
          width: 100%;
          flex-direction: column;

          &+.table-row {
            margin-top: 25px;
            border-top: 1px solid #E0E0E0;
          }

          &:hover {
            background-color: inherit;

            .table-col {
              border-color: inherit;
            }
          }
        }
      }
    }

    .table-row {
      display: flex;

      .table-col {
        padding: 15px;
        flex-shrink: 0;
        display: flex;
        align-items: center;

        .mobile-table-name {
          display: none;
          width: 100%;
          font-size: 10px;
          margin-bottom: 10px;
          letter-spacing: 1px;
          text-transform: uppercase;
          color: #909597;
          cursor: pointer;

          @media(max-width: 800px) {
            display: block;
          }
        }

        @media(max-width: 800px) {
          flex-wrap: wrap;
        }
      }

      .col-1 {
        width: 30%;
        padding: 10px 20px;

        .galaxy-name-img {
          margin-right: 20px;

          img {
            display: block;
            width: 30px;
            height: 30px;
            object-fit: fill;

            @media(max-width: 800px) {
              width: 20px;
              height: 20px;
            }
          }

          @media(max-width: 800px) {
            margin-right: 15px;
          }
        }
      }

      .col-2 {
        width: 25%;
      }

      .col-3 {
        width: 45%;
      }
    }
  }

  .no-data {
    text-align: center;
  }
</style>
