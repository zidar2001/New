<template>
  <div class="pagination text-center bg-transparent items-center justify-center sm:rounded-t text-blue-700 font-semibold  py-3 px-4 border-2 border-blue-200 rounded">
    <div class="pages content-center ">
      <button
        class="pagination_prev text-center bg-transparent  text-blue-700 font-semibold  py-2 px-4 border border-blue-700 rounded "
        v-if="localPage !== 1"
        :disabled="localPage === 1"
        @click="setPage(1)"
      >
        1
      </button>
      <button
        v-if="localPage !== 1"
        class="pagination_prev text-center bg-transparent  text-blue-700 font-semibold  py-2 px-4 border border-blue-700 rounded"
        :disabled="localPage === 1"
        @click="setPage(localPage - 1)"
      >
        Nazad
      </button>
      <button
        v-for="p in shownNumbers"
        :key="`pagination-page-button-${p}`"
        :class="p === localPage ? ' text-blue-700 font-semibold  py-2 px-4 border bg-green-500 border-blue-700 rounded  ' : 'text-blue-700 font-semibold  py-2 px-4 border border-blue-700 rounded '  "
        @click="setPage(p)"
        v-text="p"
      ></button>
      <button
        v-if="localPage !== lastPage"
        class="pagination_prev text-center bg-transparent  text-blue-700 font-semibold  py-2 px-4 border border-blue-700 rounded"
        :disabled="localPage === lastPage"
        @click="setPage(localPage + 1)"
      >
        Dalje
      </button>

      <button
        class="pagination_prev text-center bg-transparent  text-blue-700 font-semibold  py-2 px-4 border border-blue-700 rounded"
        v-if="localPage !== lastPage"
        :disabled="localPage === lastPage"
        @click="setPage(lastPage)"
      >
        {{ this.lastPage }}
      </button>
  </div>
  </div>

</template>
<script>

export default {
  props: {
    value: {
      type: Number,
      default: 1
    },
    lastPage: {
      type: Number,
      default: 1
    },
    debounce: {
      type: [String, Number],
      default: 0
    }
  },
  data() {
    return {
      localPage: 1,
      switching: false,
      timeout: null
    }
  },

  computed: {
    shownNumbers() {
      const LENGTH = 2
      const {lastPage} = this
      const page = this.localPage


      const firstPageInSight = page <= Math.floor(LENGTH / 2)
      const lastPageInSight = lastPage - page <= Math.floor(LENGTH / 2)


      const firstNumber = lastPageInSight ? lastPage - LENGTH + 1 : page - 1
      const lastNumber = firstPageInSight ? LENGTH : page + 1

      const first = Math.max(1, firstNumber)
      const last = Math.min(lastPage, lastNumber)

      const pages = []
      for (let i = first; i <= last; i++) {
        pages.push(i)
      }
      return pages

    }
  },
  watch: {
    value: {
      handler: 'setPage',
      immediate: true
    }
  },
  methods: {
    setPage(newPage) {
      if (newPage === this.localPage) return
      if (newPage > this.lastPage) return
      if (newPage < 1) return

      this.localPage = newPage
      this.switchPage(newPage)
    },
    switchPage(newPage) {
      if (this.switching) {
        clearTimeout(this.timeout)
        this.timeout = null
      }

      this.switching = true
      this.timeout = setTimeout(() => {
        this.$emit('input', newPage)
        this.switching = false
      }, Number(this.debounce))
    }
  }
}
</script>

<style scoped>
/*.pagination {*/
/*  width: 100%;*/
/*  padding: 15px 0;*/
/*  margin-top: -1px;*/
/*  font: 11px sans-serif;*/
/*  line-height: 18px;*/
/*}*/
/*.pages {*/
/*  width: 100%;*/
/*  float: none;*/
/*  text-align: center;*/
/*  display: block;*/
/*  padding-top: 25px;*/
/*  padding-bottom: 25px;*/
/*}*/
/*.pagination button {*/
/*  float: none;*/
/*  outline: none;*/
/*  -webkit-box-shadow: 0 2px 15px 0 rgba(0, 0, 0, 0.1);*/
/*  box-shadow: 0 2px 15px 0 rgba(0, 0, 0, 0.1);*/
/*  margin: 8px;*/
/*  min-width: 40px;*/
/*  height: 40px;*/
/*  text-align: center;*/
/*  border-radius: 100px;*/
/*  line-height: 39px;*/
/*  font-size: 16px;*/
/*  font-weight: 100;*/
/*  border: 1px solid rgb(238, 238, 238);*/
/*  -webkit-box-sizing: border-box;*/
/*  box-sizing: border-box;*/
/*  display: inline-block;*/
/*  font-family: Circular, Arial, Helvetica, sans-serif;*/
/*  color: rgb(51, 51, 51);*/
/*  padding: 0 10px;*/
/*  &.active {*/
/*    background: linear-gradient(*/
/*        45deg,*/
/*        rgb(253, 109, 88) 0,*/
/*        rgb(248, 140, 35) 100%*/
/*    );*/
/*    -webkit-transition: background 0.4s ease-in;*/
/*    -o-transition: background 0.4s ease-in;*/
/*    transition: background 0.4s ease-in;*/
/*    color: white;*/
/*    border-color: rgba(0, 0, 0, 0);*/
/*    border: 0;*/
/*    font-weight: bold;*/
/*  }*/
/*}*/
/*.pagination_prev {*/
/*  padding: 0 25px !important;*/
/*  width: auto;*/
/*  border-radius: 100px !important;*/
/*  font-size: 13px !important;*/
/*  font-weight: 100 !important;*/
/*}*/
/*.pagination_end_page {*/
/*  float: none;*/
/*  outline: none;*/
/*  -webkit-box-shadow: 0 2px 15px 0 rgba(0, 0, 0, 0.1);*/
/*  box-shadow: 0 2px 15px 0 rgba(0, 0, 0, 0.1);*/
/*  margin: 8px;*/
/*  min-width: 40px;*/
/*  height: 40px;*/
/*  text-align: center;*/
/*  border-radius: 100px;*/
/*  line-height: 39px;*/
/*  font-size: 16px;*/
/*  font-weight: 100;*/
/*  border: 1px solid rgb(238, 238, 238);*/
/*  -webkit-box-sizing: border-box;*/
/*  box-sizing: border-box;*/
/*  display: inline-block;*/
/*  font-family: Circular, Arial, Helvetica, sans-serif;*/
/*  color: rgb(51, 51, 51);*/
/*  padding: 0 10px;*/
/*}*/
/*.pagination img {*/
/*  padding: 0;*/
/*  border: 0;*/
/*  float: none;*/
/*  margin: 0;*/
/*  display: inline-block;*/
/*  border-radius: 5px;*/
/*}*/
</style>
